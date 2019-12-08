# Chrome-debug
#### For debugging in VS Code on the Mac: a double-clickable icon which will start Chrome with `--remote-debugging-port=9222`

I made a double-clickable icon which will start chrome in "remote debugging" mode, for use with VS Code (and maybe other things). It has the usual Chrome logo but with "9222" superimposed on it, so that it is easy to tell which is which. There are some mildly complicated instructions about how to set it up, which are included below, but in response to an issue raised by @kriscoleman I realized that the simplest thing to do was to upload a .dmg with the final product already on it. So:

#### Installation instructions:

1. Click on the "Chrome-debug.dmg" file.
2. Click "Download" on the next screen.
3. Open the .dmg file you just downloaded, e.g. by double-clicking.
4. Drag the "Chrome-debug" icon anywhere you want it (desktop, Applications folder, etc.)
5. Drag it to the dock, if you want. (Note: if you drag it directly to the dock, I think it will stop working after you eject the .dmg image.)

**Note:** When you run this, you get another instance of Chrome running with the standard Chrome icon. I.e., if you put it in the dock and click on it, you do not get the usual dot by it saying it's running.

**Other note:** This is a double-clickable app(let). There is no need to mess with bash paths, etc.

#### What's in the repo, if you want to do it the hard(er) way:

This repo contains the "Chrome-debug" app, and an icon to paste on it, which is basically the Chrome icon with "9222" written on it 
so as to remember that this is the debugging version of Chrome.

To make it work, may need to execute this shell command

`chmod +x Chrome-debug.app/Chrome-debug`

in the root of the project (I didn't, when I tested it).

Also, open `chrome-debug-icon.png` (not `.psd`) in Preview, select all, and copy. Right-click the `Chrome-debug` app > Get Info. 
Click on the small icon in the upper-lefthand corner, and hit paste. The correct icon should now be attached to the "app."

The guts of is  this one-line shell script (yes, I did not use `sudo`):

```
#!/bin/bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222&
```
#### Original question, and alternative approaches:

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

Apparently it is possible to use Automator to turn a shell script into an app [Edit: a later commenter supplied a [link to instructions](https://stackoverflow.com/a/59164839/1527750)], but before I learned that, I found out that there are 
various ways that used to work that are now broken, and one [simple way that still works](https://apple.stackexchange.com/a/269045/102436).
There is also a way to make a double-clickable shell script, but it will open a Terminal window.

It shouldn't be too difficult to build a more robust "bundle" which would not need to have the custom icon pasted on. It would involved building a bundle with a `plist` file, either by hand or by using Xcode. But that would be a project for another day. [Edit: and once I figured out that I could just put this on a dmg, this approach doesn't seem worth the bother.]

https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html

https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFBundles/BundleTypes/BundleTypes.html#//apple_ref/doc/uid/10000123i-CH101-SW1
