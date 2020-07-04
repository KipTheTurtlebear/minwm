# minwm
An ncurses based app switcher / launcher / window manager developed with the PinePhone in mind.

The name inspiration comes from the fact that the switching mechanism will revolve around the desktop analogy that when an app is selected, the minwm will be “minimized” and the app will display on the same “desktop”. Switching back to minwm from the app requires the current app to be “minimized” as well. Also, I’m following the inspiration behind SXMO and the “suckless” programs that tend to be minimalistic and do one job and do it well, so “min” is a play on that.

## All Team Member names 
Trent Wilson

## Project Overview: what will your project do? What function will it serve?
minwm will enhance the functionality of the SXMO UI. minwm will be an ncurses based app that lists the currently open gui apps. Selecting one will “switch to the app”. At first my idea was to interface with a window manager in order to implement the “switching” but after a lot of research and many different ideas I think it is feasible to code directly with the xorg api to map and unmap programs as needed.

## Project Technologies: what do you expect to use to build it? Languages, libraries, etc 
Language: C
Compiler: Need to compile for aarch64
Emulator: QEMU with postmarketOS for testing
Libraries: Potentially Xlib or XCD as well as SXMO packages
Target device: PinePhone
I’ll use SXMO UI as a starting point. minwm will eventually replace its window manager dwm. A long term goal feature of minwm will also replace SXMO’s dmenu menuing system (but that is outside of scope here). Most development wont actually depend on SXMO but to be able to use minwm on the PinePhone, other components will need to be present on the phone. SXMO’s lisgd library converts swipe gestures to any commands (like shortcuts basically). These will be useful once minwm is implemented to switch between the open app and minwm itself. Also, the onscreen keyboard svkbd will be important for text input once on the phone.

## Related Work: what is already out there that is comparable to what you are proposing? (open source and commercial) 
Currently, SXMO uses dwm as a tiling window manager with multiple desktops. The user swipes left and right to go from desktop to desktop which can have different apps on them. This is a direct application of a normal desktop computer’s tiling window manager with touch added on top. The downside of this is that if the user is on desktop 1 and there are 10 active desktops, he has to swipe through 9 apps to get where he wants to. And there is no view to see a list of everything that’s open, so it’ll be easy to forget which desktop has what he’s looking for anyway. The idea of SXMO is brilliant. However, even a desktop that is considered very basic on a traditional desktop is relatively complex when used on a device like a phone where the interaction with the device is so limited. So minwm will reduce the features of the wm by 90% but will be more usable. (no need for tiling, split windows, virtual desktops, etc)

Other opensource phone Uis are Phosh which is GNOME’s attempt and Plasma which is KDE’s offering. Then of course there are Apple and Google’s official UI’s that we have been forced to use for the past decade.

## Three-week plan to get to a runnable pre-alpha version 
Get a handle on the ncurses API, build a scrollable list in the UI and populate it with ps process info. If there is more time, filter out background processes. If there is still more time, start interfacing with x11 and figure out how to map and unmap programs from the screen.

ncurses resource:
http://tldp.org/HOWTO/NCURSES-Programming-HOWTO/printw.html

Good explanation and view on how window managers work and what I want to do.
Virtual desktops section, implementation note talks about a compelling strategy.
https://specifications.freedesktop.org/wm-spec/wm-spec-1.3.html#idm45805412385120

c library api for X11 that may be useful to get the map/unmap or max/min or whatever.
https://xcb.freedesktop.org/

## Issues and concerns 
    • How do I differentiate between gui processes and background processes?
        ◦ What characteristic of the process notifies X that it is renderable?
        ◦ This information must be somewhere, and I need to find it.
        ◦ X11 must use something
    • How will I map and unmap incoming and outgoing active processes with x11?
