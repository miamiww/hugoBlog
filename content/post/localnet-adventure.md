+++
title = "Localnet Adventure!! Reference Page"
author = "alden"
date = 2018-09-13T14:33:27-04:00
draft = false
tags = []
categories = []
+++

![](https://s26913.pcdn.co/wp-content/uploads/2017/12/business-hackers.jpg)
You can download the slides [here](https://www.dropbox.com/s/qzp5lny2b4xmg5o/localnetadventure2.pptx?dl=0)

## Some Useful Command Line Commands
* `man` - opens the manual for a command
* `pwd` - prints the working directory, i.e. shows you where you are
* `ls` - lists the files and directories in a given directory. default is working directory
* `cd` - changes directory
* `cat` - prints the contents of a file
* `echo` - prints exactly what you give it
* `ssh` - secure shell, creates a secure shell connection to another machine
* `touch` - creates a file
* `mkdir` - makes a new directory
* `rm` - deletes a file (remove), or a directory when given the flag -r
* `mv` - moves a file to another directory, can be used to rename a file
* `cp` - copies a file
* `nano` - default command line text editor
* `|` - pipes the results of one command to another

In this exercise you will mostly be using `ssh`, `ls`, `cat`, and `cd`

## Basics of command line interface
Commands frequently have the following format:
[command] [object]

```
cat readme.txt
```
```
ssh level0@192.168.0.100
```
Some commands can take no object

```
ls
```
Commands can also be given flags, which take the form of a - or --

```
rm -r /home/directory_of_files_I_hate
```

use `man` to get a command's list of possible flags and their effects

```
man rm
```

## Important and Useful Software
* [Herbivore](github.com/samatt/herbivore/releases)
* [Homebrew](https://brew.sh)
* [Fish shell](https://fishshell.com/)
* [OhMyZsh](https://github.com/robbyrussell/oh-my-zsh)
* [Atom](https://atom.io/)
* [Visual Studio Code](https://code.visualstudio.com/)
* [Vim](https://www.vim.org/)
* [tmux](https://medium.com/actualize-network/a-minimalist-guide-to-tmux-13675fb160fa)

## Note on text editors, programming culture
You'll hear a lot about text editors and developers give each other a ton of toxic bullshit about which text editor is the best. Text editors started essentially just to let you write files, but because they are the tool for writing code they have ballooned into huge powerful programs with tons of add ons and stuff.

I would recommend either Atom or Visual Studio Code (both linked above). These are separate programs off the command line that are great and you can keep with them for forever. Command line text editors like Vim and Emacs are great and powerful but arcane and abstruse, don't listen to anyone who tell you that you need to use one of those. That being said I mostly use Vim and I love it, but it took me 3 months of a painful learning curve to get used to it. Nano is the basic command line text editor that comes with Mac and will be totally fine to use if you ever have to make little edits to a file from the command line.

Basically, and this is important, programming full of gatekeeping, and shitty asshole developers want to make you feel bad or inferior because it reinforces to them just how magic and impressive or something that they are. Push back on that and just remember that it's always OK not to know something. Remember this when you too become a 1337 hacker.


## Tips and tricks for the world outside of this simulation
* `~/` references the home folder regardless of where you are in your computer's filesystem. the home folder is usually the one with your name or whatever you decided to call it when you first set up your computer. For me my home folder is /Users/aljones/. Thus
```
touch ~/newfile.txt
```
will create a new file called newfile.txt in /Users/aljones
* if you decide to use bash, you can make a file called .bash_profile in the home folder that will run every time you open a terminal window. putting code in here is a great way to configure your workflow. you can see my bash profile [here](https://github.com/miamiww/importantdots/blob/master/.bash_profile)
* tab completion is extremely useful. I'm not sure how to explain it well, check [here](https://en.wikipedia.org/wiki/Command-line_completion). Basically if you start typing out something on the command line and hit `tab` it will complete whatever you were typing or give you a list of options
* git and github are great and wanting to use git was my rabbit hole into learning the command line. git, like all command line tools, is arcane and confusing and you can only get used to it by practice.
* you might have heard the term IDE, which is Integrated Development Environment. This is usually an application for writing a specific programming language. Xcode is a classic example. Text editors like Atom straddle the line between general text editors and general purpose IDEs.
* if you have atom installed you can open an entire directory and all of the files and subdirectores in it by navigating to that directory and typing `atom .` The period, `.` on the command line usually references "everything". `open .` will open the folder you are in in finder.
* if you want to get more into servers, you can get an account at [digital ocean](https://www.digitalocean.com/) and set up a cheap remote virtual cloud server. you connect to the server the same as here, with `ssh`. Ask me or Shawn Van Every for more info.


## References and Resources
* American Artist’s [Black Gooey Universe](http://unbag.net/issue-2-end/black-gooey-universe/)
* [Command Line Bullshit](http://www.pgbovine.net/command-line-bullshittery.htm)
* OverTheWire’s [Bandits](http://overthewire.org/wargames/bandit/)
* AT&T’s genuinely amazing [Guide To the Unix Operating System from the 1970s](https://www.youtube.com/watch?v=tc4ROCJYbm0)
* Dhruv Mehrota’s [Othernet](http://othernet.xyz/)
* [NYCMesh](http://nycmesh.net/)
* Dan Phiffer’s [Occupy.here](http://occupyhere.org/)
* Wifi art of [Third Space Collective](http://www.th1rdspac3.com/)
* France Telecom’s [Minitel](https://en.wikipedia.org/wiki/Minitel)
* Alternate Reality Games (e.g. [geocaching](https://www.geocaching.com/play))
