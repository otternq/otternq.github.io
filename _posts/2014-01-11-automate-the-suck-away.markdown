---
layout: post
title: "Automate the Suck Away"
date: "2014-01-11 21:22:00"
tags: ["bash"]
---

Last week I started at a new company as an Android developer, and within 4 days I had my nick name (ironically not Nick): "script whore"...okay, I can deal with that.

Why did I get that name? Mainly because I wrote a bash script for damn near everything a teammate or I would have to do multiple times.

After getting my computer and installing all the Android tools (I will probably automate that next), I opened up the project and read the README file. It was decent as far as instructions go, just a paragraph saying what libraries are required and what you need to run in terminal to get the project ready. So after following the instructions and finding a few missing steps I updated the README and made sure to add more details. Then I decided that I really didn't want to read that file again...so I wrote a bash script that would set the project up for anyone running a Mac (thanks [HomeBrew](http://brew.sh) - I guess Linux guys will just have to use `apt-get`).

Next I was given a run down of how the team uses _TestFlight_ which is an amazing Beta tool with very granular permissions and a really nice interface. It wants you to login, upload the package, choose a distribution list, and decided if you want to email everyone who has access to the most recent version. Same steps every time? Available API? You know where I'm going with this. So that script uploads to _TestFlight_, asking me if I want to send emails or not, then adds a comment to the ticket that build was for (its like: Hey guys, I didn't want to email you but heres a new build). The best part of this script? I was able to send it over to the iOS team and all they had to do was change the file to be uploaded. _TestFlight_ did a great job with their Upload API.

Those scripts took maybe an hour, total, and now I don't have to interrupt my work to push a build. I decide, hey this should go to _TestFlight_...run the script, and go back to work. Sometime that breaks down to "Up Arrow" > "Enter".

I took this a step further that night sitting bored in my hotel room. I installed Hubot and set it up with the chat system of choice. Now we can send [httpcat](http://httpcats.herokuapp.com/304.jpg) messages to the group, or you know **share a ticket number in the chat** and the bot runs off and gets a **summary to display to everyone**. Next I'm going to have Hubot make tickets for me so that when we're all talking about a feature/bug I can just type `hubot ticket new "awesome new feature"` and never have to leave the conversation. Also it will make sure that there aren't duplicate tickets because everyone will know its been documented.

Whats next:

- having hubot make tickets for me
- seeing about making a company boxen so no one has to install android sdk and such again