# Tr3nch
Tr3nch is an exploit allowing you to open a menu on various "chrome urls" to perform
various actions that a normal extension is not capable of doing, and is kind of like
the spiritual successor to the "Swamp ULTRA" exploit due to its behaviour and the
fact that goguardian users are guarunteed to be able to do this. It utilizes a bug
in chrome urls to allow for code execution with access to the chrome API (this bug
has been dubbed "Sh0vel") and abuses this bug to do a number of things, including:
- Adding gmails regardless of policy
- Open a webview proxy invisible to some filters
- Edit network settings for any network
- Loopkill/Disable extensions
- Run code on the page and extension with API access
- Update the device and pause/resume automatic updates

And more.

It is very unlikely that this exploit will ever be patched, as it entirely revolves around Sh0vel, which itself entirely revolves around the extensions-on-chrome-urls flag, and is technically just an automated version of the Point-Blank exploit, which Google also did not patch (unless you count the R115 bookmarklet restrictions) due to it being technically intended behaviour.
However, Google has patched Skiovox in ChromeOS release R121, breaking the setup chain. While it possible to downgrade to R120 currently to set it up, it is likely you won't be able to do this forever. The only part that matters is that you have code execution in an extension and it runs the contents of installer.js, wether you do that through DNS spoofing, XSS, or something else does not matter.

### Usage
Warning! This exploit might be difficult to setup if you do not have at least some experience with exploits like skiovox breakout and sh0vel! If you are technically challenged, this might not be the best exploit for you.

Usage is fairly straight forward:
- Find an extension capable of executing Sh0vel. Some known ones are GoGuardian and Equatio, but to see if another potential extension is vulnerable, open its manfest and verify that "manifest_version" is set to 2 (3 WILL NOT WORK!), verify that "unsafe-eval" (NOT "wasm-unsafe-eval", that will NOT WORK!) is in the "content_security_policy" tag at least somewhere (This does not count if it is in the "sandbox" attribute that will not work!), and that "activeTab" is in the list of permissions.
- Set up Skiovox Breakout on the extension. See [this guide](https://rentry.co/pm6ta) on how to do that.
- On this repo, copy the contents of `tr3nch.js`, open the page you bookmarked for skiovox breakout (if you cant open it normally, right click the bookmark and select "Open in New Tab"), paste the contents into the textbox, and press evaluate.
- Tr3nch is now set up on this extension. When the extension restarts (e.g. from signing out/in, killing it and disabling it, or deloading tr3nch), tr3nch will be unloaded, and can be reloaded by opening the skiovox breakout page (Yes you HAVE to open it first!) and changing the url to `filesystem:chrome-extension://id_for_the_extension_here/temporary/evaluations/index.html`. If you ever run something other than tr3nch from skiovox breakout you will need to redo the setup.
- Once tr3nch is set up, go to any "chrome url" (The best of which being chrome://extensions, chrome://chrome-signin, chrome://os-settings, chrome://settings, and chrome://file-manager) and clicking the icon of the extension you injected tr3nch into in the top right menu.

### Credits
- Zeglol1234: The idea, main developer
- Writable: Skiovox Breakout implementations (Not affiliated with this project directly)
- Bypassi: Add gmails exploit (Not affiliated with this project directly)
- Notboeing747: Misc development and testing
- Kxtz: Misc development and testing
- Archimax: GUI inspiration
- Kelsea: The logo
- Katie: Testing
- The rest of Whelement: Mental support
