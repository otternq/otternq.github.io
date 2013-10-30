---
layout: post
title:  "Installing MongoDB on a Mac"
date:   2013-10-28 19:00:05
tags: ["Mac", "MongoDB", "MacPorts"]
---

Upgrading MacPorts
----

I'm working on a couple of projects that require _MongoDB_, but I have not worked with _MongoDB_ on a Mac before, so I'm installing it on my computer. Right at the beginning I was unable to install _MongoDB_ with _MacPorts_, which I then tried to upgrade to see if my system was just out of date. That failed. I couldn't upgrade _MacPorts_ which was solved by `sudo xcode-select --install` after `sudo port -d selfupdate` told me I didn't have Tcl. So grate, _MacPorts_ is now up to date, time to update my _MacPort_ packages.

Apparently there was a lot to update because it took about 30 minutes.

Notes
----
- [Stackoverflow](//stackoverflow.com) fixed the _MacPort_ update issue for me, here is the [question](http://stackoverflow.com/questions/19622337/cant-update-macports-with-mac-os-x-mavericks).