---
layout: post
title:  "Installing MongoDB on a Mac"
date:   2013-10-29 19:00:05
tags: ["Mac", "MongoDB", "Homebrew", "MacPorts"]
---

Upgrading MacPorts
----

I'm working on a couple of projects that require _MongoDB_, but I have not worked with _MongoDB_ on a Mac before, so I'm installing it on my computer. Right at the beginning I was unable to install _MongoDB_ with _MacPorts_, which I then tried to upgrade to see if my system was just out of date. That failed. I couldn't upgrade _MacPorts_ which was solved by `sudo xcode-select --install` after `sudo port -d selfupdate` told me I didn't have Tcl. So grate, _MacPorts_ is now up to date, time to update my _MacPort_ packages.

Apparently there was a lot to update because it took about 3 hours. Even then, _MacPorts_ failed to install _mongodb_.

Continuation (2013-10-30)
------
Installing _MongoDB_ still failed after all of the udpates to _MacPorts_...so now its _homebrew_'s turn. (After recomendation from [@vangnol](https://twitter.com/vangnol))

So, I uninstalled _MacPorts_ with the [guest](http://guide.macports.org/chunked/installing.macports.uninstalling.html) from _MacPorts_ own manual, and installed _homebrew_ with: `ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"`

I also had to make sure that some paths in my PATH variable were ordered correctly, check `brew doctor` for any fixes that your system may require.

After _homebrew_ installed and my PATH fixed, I closed and re-opened my terminal and installed _MongoDB_ with `brew install mongodb`. It took about 10 minutes, and I'm now up and running.

Notes
----
- [Stackoverflow](//stackoverflow.com) fixed the _MacPort_ update issue for me, here is the [question](http://stackoverflow.com/questions/19622337/cant-update-macports-with-mac-os-x-mavericks).