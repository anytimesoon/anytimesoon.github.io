---
layout: post
title:  "Bash on Windows"
date:   2017-06-21 19:58:05 +0000
---


I'm a windows guy. I just don't like OSX and linux doesn't have enough variety of software. Windows is far from perfect, but it's always been my OS of choice. I love it even more since the release of the surface line of hardware. The surface book is the best laptop I've owned, and I wasn't going to let a small thing like quitting my job and becoming a ruby dev get in the way of my favourite things! Ruby seems to run best on unix machines, it seems. 

A couple years ago, this might have been a problem, but Microsoft announced Bash on Windows with the release of Windows 10. From what I've read, there were quite a few bugs with it when it was first released, but they seem to have been mostly ironed out. Below, I'll talk about how I got started, what I've tried, what works and what doesn't.

# How to install
[This is the tutorial I followed](https://gorails.com/setup/windows/10). I'm sure there are plenty of others out there, too, so I won't rehash that on this blog. I had troubles with rbenv, so went with rvm instead. This seems to work well for me.

You should now have ruby on rails running in linux running in windows. Great! Now you just need something to code in. I like sublime text. [Installation instructions here](http://tipsonubuntu.com/2015/03/27/install-sublime-text-2-3-ubuntu-15-04/). Bare in mind that whichever text editor you choose needs to be installed in the linux environment using the bash shell.

By this point, I'm sure you've already started a new rails app, moved into the new directory and run ```subl .``` and nothing happened. This is because we're only officially given the linux terminal, so there is where things get a little hacky. You'll need to install [this](https://sourceforge.net/projects/xming/) software, which will allow you to run a graphical app from your linux subsytem to show up in the windows environment.

# What doesn't work
Your mind should be well and truly blown at this point (mine is). So let's cool off a bit by going through the bits that don't work quite so well. 

Not all apps launch with xming. I have tried a couple IDE's (vs code, and atom) and neither will launch. This is a known bug, so hopefully it will be fixed in the near future.

Copying and pasting is a little buggy. The clipboard can get a little confused sometimes, when copying from windows and pasting to linux (but not the other way around, for some reason)

Modifying linux files from the windows environment. DO NOT DO THIS. If you do this, you're going to have a bad time. Believe me. I tried using VS Code (windows installation) and running the bash shell inside it. That works really well until you start actually doing any work, and nothing gets saved. You have been warned.

# What I'd still like to try
You can actually run bash right from the powershell! [That doesn't make any sense](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS1aVsrpLclbivPWfhTmnLbd8YB0MKoeMmLRumKG3j182Y5dPVO)

This might be useful if you want to run an ide in the windows environment. When you run ```bash``` in powershell you don't have access to the linux subsystem filesystem. [WHAT?!?!?](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQXyAoUuHXHVPQZUjYDPQ1nY6ybvqlP9KOgXwxSS76_u6clL9sr) So I guess this might be useful to run bash commands in the windows environment, but at this point my brain has exploded and I don't know how anything works anymore. 
