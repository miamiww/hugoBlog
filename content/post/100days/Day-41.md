+++
title = "Shodan Stories Day 41: Mining for Innovation in Abu Dhabi, Trapped in the Multiverse of Project Validation, Haunted by the Lightbulb of Ideas, Tasked with an Eternity of Teamwork Communication Adjustment"
date = 2019-02-13T23:19:12-05:00
draft = false
tags = []
categories = ["100 days"]
+++

I saw someone searching for "snapchat" today. "YOLO", I said to myself, and dived in.

## Fujairah Innovation Mine on 83.111.19.71
The search was in fact pulling up some of Snapchat's production servers. Those were fairly boring however, though I did find something a little more interesting.
![](/images/100Days/Day41/firstlook.png)
This is a website for an organization called Fujairah Innovation Mine, which seems to be a typical tech startup incubator. The website was was running on port 7548 of the IP, so it clearly couldn't be the official version. I found that it was running the exact same website on port 80 though, so maybe this one was just for testing. And then I did an `nmap`, and I found it was running the same exact website on port 81, and port 82, and port 83, 84, and port 1000, and port 1200, and port 1234, and port 2000, and port 5985, and port 8000, and port 23000, and port 61199, and well you get the idea. If every open port was running a web server running this website then there seem to be least 65,000 iterations of the same exact website. Yes _65,000_. No I didn't check them all, though I checked about 100 and they were all running it. Yes that's almost every possible port. No they weren't redirects. And no there were no differences between any of them as far as I could tell.
![](/images/100Days/Day41/mine.png)
Why??? What could even cause this???? I couldn't find any answer. I almost sent them an email but didn't know how to explain myself.

Well I guess I deserve this for saying yesterday that some mysteries are better left unsolved. See you tomorrow.
