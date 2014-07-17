---
layout: post
title:  "Security with PI"
date:   2014-07-16 22:25:00
tags: ["raspberry", "pi", "camera", "security"]
---

#Security Cams with Raspberry PI

The only interesting projects have to do with MEMEs, just kidding, I love a
project that has real life implications. Software used to make someones life
more interesting or easier is by far more rewarding to work on than a little
terminal app I wrote during a string of late nights.

> Not discriminating against memes, I have my own MEME generator
  [TerMEME](//github.com/otternq/termeme), so there is still much love.

##The Start

My uncle called while I was doing some laundry on Wednesday, he had been spending
some time following a couple tutorials attempting to setup a home security system.

Kick Ass! Probably should have asked why he needed security cameras, but nerds don't
seem to be to curious about RL aspects like that. We drove right into debug mode.

He'd managed to do the entire install process and get it working so that he could
access the camera by his iPhone via the PI, but it failed to restart when the
PI rebooted. Rather common situation, especially for someone which minimal Linux
experience.

After a couple failed attempts at trouble shooting over the phone, we decieded it
was time to give me access to the PI (we're in different parts of the state) and
set up a port forward. Within a couple commands I had the camera accessable by
the iPhone again...but full capacity after a reboot continues to elude us.

By had we are able to get the setup working with two commands, and we've twice had
everything setup correctly on boot, but consistency eludes us.

Time for a more methodical approach.

> **Side note: **
> If your going to be working on remote programming problems like this, get into
> the habit of using `script` and `screen`. `script` is awesome for showing how
> you approached and solved a problem, while `screen` is great for being setup
> super similar each time you `ssh` into their box.

##Starting over

**Raspberry PI's** use SD cards for their storage, this is awesome because starting
from scratch costs almost nothing and your able to be back at your stable point almost
immediately. I didn't want to lose all the hard work my undle did, he made it a long
way down the install path and its working about 90% so to throw it way would be horrible.
However I dod want a fresh start so we can document our steps better and get a more comprehensive
viewpoint of the PI's setup.

So we got a new SD card, formated it with Wheezy and started from script. This time taking
notes (both paper and `script`) so we can re-create this as many times as we wish.
Additionally the notes may help us to script portions of the setup process which
is my personal learning goal from this project. I keep attempting to automate the
shit out of everything.
