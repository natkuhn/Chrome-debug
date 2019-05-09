# Chrome-debug
#### For debugging in VS Code on the Mac: a double-clickable icon which will start Chrome with `--remote-debugging-port=9222`

This is an answer to the following [question on Stack Overflow](https://stackoverflow.com/questions/56043142/enable-remote-debugging-on-chrome-by-default-on-mac):

>### Enable remote debugging on Chrome by default on mac?
>
>I am working on getting the VS Code debugger to attach to Chrome as part of my regular workflow.
>
>I keep Chrome running all the time, and the highly-regarded VS Code Live Server extension opens my project in a new tab, which I like. 
I would like to be able to attach the VS Code debugger to this instance, but it looks like I have to start Chrome from the command line with
>
>```
>sudo /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222
>```
>Several questions:
>
> 1. Is there a way to modify Chrome's configuration file so that it always starts with that flag set?
> 2. Is that a stupid thing to do?
> 3. Do I really need the `sudo` in the line above? Some sources do not have it.
> 4. Alternatively, is there a way to create a desktop/toolbar shortcut to chrome that will start it will remote debugging enabled?

Apparently it is possible to use Automator to turn a shell script into an app, but before I learned that, I found out that there are 
various ways that used to work that are now broken, and one [simple way that still works](https://apple.stackexchange.com/a/269045/102436).
There is also a way to make a double-clickable shell script, but it will open a Terminal window.

This repo contains the "Chrome-debug" app, and an icon to paste on it, which is basically the Chrome icon with "9222" written on it so 
remember that this is the debugging version of Chrome.

To make it work, you will probably need to, in the root of the project:

`chmod +x Chrome-debug.app/Chrome-debug`

Also, open `chrome-debug-icon.png` (not `.psd`) in Preview, select all, and copy. Right-click the `Chrome-debug` app > Get Info. Click 
on the small icon in the upper-lefthand corner, and hit paste. The correct icon should now be attached to the "app."
