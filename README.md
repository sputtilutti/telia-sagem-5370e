# Telia Router Sagem 5370e personal settings

Overrides and stuff for my Sagem F@st 5370e router


# Swedish åäö characters in SSID

I wanted a SSID with Swedish åäö chars (and &), but the Sagem/Telia interface does not allow me to input such chars.
According IEEE 802.11-2012 (Section 6.3.11.2.2), SSID can be 0-32 octets with an unspecified or UTF8 encoding - so I should be allow to use whatever I want.

The SSID string validity check is done using Javascript. Fortunately that can be overridden, and Chrome helps you do it in a very convenient way!


## Override SSID string check

1. Login into the web interface as Administrator user.
2. Go to the wifi settings.
3. Using Chrome, open Inspect interface and go to sources and open the Override pane. 
4. Create a new directory where you want to store your overridden files.
5. Go back to Page pane and righ-click on the file you want to override, in this case it is the `config.js%XXX...` where "XXX..." is a string that the router generates each factory reset I think.
6. Select 'Save to override'.
7. Still in Inspect, open the new override config.js file from Override pane.
8. Chrome allows you to prett-print the json file so do that by clicking on the `{}` in bottom of edit-pane.

Now, we want to modify `ssidKeyRules` and `wifiForbiddenChars` variables in the JSON config file.
Simply search for them and edit it according to the below

before

    < ssidKeyRules: /^[a-zA-Z0-9$@^`,|%;.~()\/\\{}:?[\]=\-\+_#!><]{8,63}$/,
    < wifiForbiddenChars: /[\"ßº§äöü]/i,

after

    > ssidKeyRules: /^[a-zA-Z0-9$@^`,|&%;.~()\/\\{}:?[\]=\-\+_#!><]{8,63}$/,
    > wifiForbiddenChars: /[\"ßº§ü]/i,

and save the file (cmd+S) and then refresh the page. Note that you need to keep the Inspect window open for Chrome to override the file.

You can now use åäö and & in the SSID name.
