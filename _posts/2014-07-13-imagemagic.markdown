---
layout: post
title:  "Preparing Imagemagic"
date:   2014-07-13 17:45:00
tags: ["imagemagick", "meme"]
---

# Preparing Imagemagic

I'm going to be using __Imagemagic__ for a project which requires
some image manipulation, fun stuff. Turns of to be a bit of a process to
get everything I want setup properly.

## Installing Imagemagic

Installing __Imagemagic__ is simple enough thanks to __Homebrew__,
a one liner actually:

```bash
brew install imagemagick
```

## Setting up fonts

The fun part comes when attempting to setup fonts for __Imagemagic__,
where you must create a _type.xml_ which stores all the fonts you
wish __Imagemagic__ to be capable of using.

Luckily for us, a [_perl_](http://www.imagemagick.org/Usage/scripts/imagick_type_gen)
script is provided to setup _type.xml_ in one step. Except
the portion where it didn't work automatically on my _Mac_ when I
simply ran `perl imagick_type_gen`, less than awesome. What ended
up working for me was piping a list of files into _imagick_type_gen_
with `find /Library/Fonts -name '*.ttf'`.

Ending up with:

```bash
find /Library/Fonts -name '*.ttf' | perl imagick_type_gen -f - > ~/.magick/type-myfonts.xml
```

## A little cleanup

I need to setup the fonts in _type.xml_, and for that in need the
*imagick_type_gen* perl scrupt...but only just once...theres no need
to keep it around afterward.

So I've written a little ruby script which takes care of downloading the
perl script, generating _type.xml_, and then deleting the perl script.

```ruby
`mkdir -p ~/.magick`
`curl -fsSL http://www.imagemagick.org/Usage/scripts/imagick_type_gen > imagick_type_gen`
`find /Library/Fonts -name '*.ttf' | perl imagick_type_gen -f - > ~/.magick/type-myfonts.xml`
`rm imagick_type_gen`

`touch ~/.magick/type.xml`

File.open("#{ENV["HOME"]}/.magick/type.xml", 'w') do |f|
  f.write '<typemap>
    <include file="type-myfonts.xml" />
</typemap>'
end

```

and to take it one step further here is a one liner to prepare
fonts for __Imagemagic__:

```bash
ruby -e "$(curl -fsSL https://raw.github.com/otternq/termeme/master/script/systemdeps.rb)"
```

##All done

So, some Goolge searches later I've gotten two lines for
**ImageMagick**, one to install it and one to prepare the
semi-required _type.xml_ file.

I think for the next step I'll update the script to allow a user
to provide the directory where their fonts are stored.
