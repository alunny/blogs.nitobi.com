---
layout: post
title: PhoneGap Blackberry on OS X
categories: [blackberry, phonegap]
---
![BlackBerry Simulator in OS X][simulator-image]

Nitobi/PhoneGap dev Fil Maj [tweeted][fils-tweet] the other day about [this excellent tutorial from Aziz Uysal][tutorial], describing how to get the BlackBerry SDK and simulator up and running on OS X, for which it has no official support. Using some Eclipse skills and Wine magic, you can pull up the simulator and enjoy all the benefits of BlackBerry dev without booting up a VM.

If you want to run PhoneGap-BlackBerry in this environment, it’s trivially easy. Here’s how:

1. Do everything it says in the tutorial, until you can run a Hello World app in the simulator
2. Clone the [PhoneGap-Blackberry][repo] repo
3. File -> Import… -> General, Existing Projects into Workspace, then Next
4. Under Select root directory, select `/whatever_your_path_is/phonegap-blackberry/framework/` and then select PhoneGap in the Projects field below
5. Add an `index.html` file to the `src/www` directory.
6. Open `build.xml` for editing. Change the `jde.home` and `simulator.home` properties to match your simulator location (if you follow Aziz’s tutorial, you can copy these properties from the `build.xml` of that project). Edit the `load-simulator` tag (`<target name="load-simulator">`) to match the other `build.xml` file also
7. Drag `build.xml` into the app view (as detailed in Aziz’s tutorial). Then double-click on load-simulator
8. Hit Menu (next to the green button), then Downloads, then PhoneGap
9. Hrrm... ??????????
10. Profit!

Thanks to Aziz for writing such a great tutorial – now we just need someone to get XCode running on Windows 7!

**Edit**: This tutorial was [previous referenced][mailing-list] on the PhoneGap mailing list by John Britton – I wasn’t aware until he brought it up in a later message. Thanks for bringing this to our attention John.

[simulator-image]: /images/phonegap-blackberry-osx.png "BlackBerry Simulator, running in Wine"
[fils-tweet]: http://twitter.com "@filmaj"
[tutorial]: http://www.azizuysal.com/2009/07/blackberry-development-on-mac-os-x.html "BlackBerry Development on OS X"
[repo]: http://github.com/phonegap/phonegap-blackberry "PhoneGap BlackBerry Repo"
[mailing-list]: http://groups.google.com/group/phonegap/browse_thread/thread/ebd3681c8eefba3d/eb29373d7606be8f?lnk=gst&q=blackberry+os+x