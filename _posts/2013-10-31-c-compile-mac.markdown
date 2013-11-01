---
layout: post
title:  "Compiling C/C++ on OSX Maverick"
date:   2013-10-31 16:00:00
tags: ["c++", "gcc", "g++"]
---

The Problem
-------
I've been working on my compiler for the instructional C- language and I've started to run into a few warnings (while compiling my compiler); clearly not something I want. Warnings are sloppy, and I think that my teacher's automated tests expect your _makefile_ to run without warnings. So, I want to make sure that I don't get any errors/warnings...specifically on the system my teacher is testing on; so I upload my code to the Computer Science server to see if I get the same errors there. 

None. No warnings on the school's system.

Um. Okay, its the same _makefile_ on both machines, so both compiles were ran with _g++_ like I specified right? Again, no. _GCC_ on my Mac is actually running _clang_ (_LLVM_).


On My Mac
-------

Here is the terminal output for how OSX compiled my program and the output for _gcc_.

###compilation

{% highlight bash %}
$ make
bison -v -t -d c-.y
flex c-.l  # -d debug
g++ -DCPLUSPLUS -g   -c -o lex.yy.o lex.yy.c
clang: warning: treating 'c' input as 'c++' when in C++ mode, this behavior is deprecated
g++ -DCPLUSPLUS -g   -c -o c-.tab.o c-.tab.c
clang: warning: treating 'c' input as 'c++' when in C++ mode, this behavior is deprecated
g++  lex.yy.o c-.tab.o -ll -lm  -o c-
{% endhighlight %}

###gcc/g++ version

{% highlight bash %}
 gcc --version
Configured with: --prefix=/Applications/Xcode.app/Contents/Developer/usr --with-gxx-include-dir=/usr/include/c++/4.2.1
Apple LLVM version 5.0 (clang-500.2.79) (based on LLVM 3.3svn)
Target: x86_64-apple-darwin13.0.0
Thread model: posix
{% endhighlight %}

On School Server
-----------

Here is the terminal output for how my school server (some linux) compiled my program and the output for _gcc_.

###compilation

{% highlight bash %}
$ make
bison -v -t -d c-.y
flex c-.l  # -d debug
g++ -DCPLUSPLUS -g   -c -o lex.yy.o lex.yy.c
g++ -DCPLUSPLUS -g   -c -o c-.tab.o c-.tab.c
g++  lex.yy.o c-.tab.o -ll -lm  -o c-
{% endhighlight %}


###gcc/g++ version

{% highlight bash %}
$ gcc --version
gcc (GCC) 4.4.7 20120313 (Red Hat 4.4.7-3)
Copyright (C) 2010 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
{% endhighlight %}

Enter Brew
--------
Earlier this week I transitioned from _MacPorts_ to _Brew_, so with _gcc_/_g++_ being wrappers to _clang_ on my computer, it seemed like a good time to see what _Brew_ could offer me for _gcc_. 

{% highlight bash %}
$ brew search gcc
apple-gcc42  gcc43    gcc44        gcc45        gcc46    gcc47        gcc48    gcc49    llvm-gcc28

If you meant "gcc" precisely:

GCC is now maintained in homebrew-versions, with major version
number in formula name as suffix. Please tap using:

    brew tap homebrew/versions

and then install GCC based on its version, e.g., 'brew install gcc47'.
homebrew/dupes/apple-gcc42
{% endhighlight %}

because of [3 tips for coding with maverick](http://blog.new-bamboo.co.uk/2013/10/24/3-quick-tips-for-coding-with-os-x-10-9-mavericks), I chose to use *apple-gcc42* with `brew install apple-gcc42`

Now with with the installtion complete, I have `gcc-4.2` and `g++-4.2` commands, and with the version flag:

{% highlight bash %}
$ gcc-4.2 --version
i686-apple-darwin11-gcc-4.2.1 (GCC) 4.2.1 (Apple Inc. build 5666) (dot 3)
Copyright (C) 2007 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
{% endhighlight %}

Finally, compiling my program does not generate any warnings and I no longer need to test each step on the University servers:

{% highlight bash %}
$ make
bison -v -t -d c-.y
flex c-.l  # -d debug
g++-4.2 -DCPLUSPLUS -g   -c -o lex.yy.o lex.yy.c
g++-4.2 -DCPLUSPLUS -g   -c -o c-.tab.o c-.tab.c
g++-4.2  lex.yy.o c-.tab.o -ll -lm  -o c-
{% endhighlight %}

Notes
------
- I had to reinstall _gmp4_ (`brew reinstall gmp4`) because it was compiled with _libstdc++_ and Maveriks now uses a different library _libc++__. See [Homebrew C++ standard libraries](https://github.com/mxcl/homebrew/wiki/C++-Standard-Libraries) and [3 tips for coding with mavericks](http://blog.new-bamboo.co.uk/2013/10/24/3-quick-tips-for-coding-with-os-x-10-9-mavericks) for more details.
- _Homebrew_ takes forever to install _gcc_ ... so plan for that