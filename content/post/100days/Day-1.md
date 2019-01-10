+++
title = "Shodan Stories Day 1"
date = 2019-01-04T11:06:35-05:00
draft = false
tags = []
categories = ["100 days"]
+++

A note up front:

Generally I've been struggling with an ethical question of this project, should I be publishing the IP addresses and personal identification of individual people I find? I can't imagine that anyone reading this would take that info and do anything untoward with it, but it's an odd stance on surveillance culture to dox strangers meaninglessly, even if the ability to reach out and randomly touching a stranger is the reality of networked existence. Currently I'm erring on the side of publishing IPs, since they are an important part of my process and should be documented, and then including anything from WhoIs records as is valid to the project, since WhoIs is meant to be public record. Things like hacker tags and defacements that I find I definitely will publish though. Happy to get input on this.

### An Open VNC Server on 204.12.214.178
![](/images/100Days/Day1/OpenVNCServers.png)

Day 1 I'm starting with some low hanging fruit: looking for people who've left VNC servers running without passwords. [VNC (standing for Virtual Network Computing)](https://en.wikipedia.org/wiki/Virtual_Network_Computing) is a framework for remotely logging into a computer using a GUI, and is a common alternative to ssh for people who don't know how to use the command line or need GUI functionality on their remote machine. To do this on Shodan I searched for IPs with port 5900 open, since VNC typically runs on 5900, and then just started trying to connect using [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/) as a client. Well the second result I found on Shodan didn't have a password and had already been totally overrun with trolls leaving each other notes and tearing apart the server. When I first logged in someone had drawn a bunch of swastikas in MS Paint and made it the background of the desktop, which I quickly changed, and someone else was playing solitaire. The server was running Microsoft Windows Server 2000 as its operating system, so it had a bunch of the classic 1999 features of Windows like MS Paint and grey boxes UI. It was a little nostalgic.

![](/images/100Days/Day1/Windows2000.png)
Looking around I got kind of nervous because I could tell other people were also in this machine. It's uncomfortable to be in a computer with a bunch of other people, at least one of whom is a nazi. Whoever was playing solitaire was clearly very engaged because they kept pulling the window back to the front.
![](/images/100Days/Day1/Defacement1.png)
![](/images/100Days/Day1/Tag.png)
Some hacker going by `yellows111` had left a tag. It looks like they use that tag a lot and I found their twitter, github, soundcloud, steam account, youtube, etc.  They have a [bot of them that you can add to your discord server](https://yellows111.github.io/) so if you want you can have yellows111 in your life at all times. Judging from their Youtube [they like to go around trashing old Windows servers](https://www.youtube.com/watch?v=97vRVU-UO6w) and might have been the one playing solitaire.

The man who owns this server lives in Missouri and purchased the server space from [Wholesale Internet](https://www.wholesaleinternet.net/). I think he's getting ripped off, at minimum $10/month for a server running an almost 20 year old operating system is pretty bad.

There were some more mysteries though that are up to the reader to interpret. Here is a traceroute result from me to the IP. What's onliare.com? It doesn't resolve to anything in a browser.

```
traceroute to 204.12.214.178 (204.12.214.178), 64 hops max, 52 byte packets
 1  192.168.0.1 (192.168.0.1)  2.529 ms  1.650 ms  1.168 ms
 2  * * *
 3  be61.nycynymy02h.nyc.rr.com (68.173.202.74)  15.107 ms  11.720 ms  15.173 ms
 4  agg113.nyquny9101r.nyc.rr.com (68.173.198.42)  16.422 ms  18.154 ms  19.666 ms
 5  bu-ether15.nycmny837aw-bcr00.tbone.rr.com (66.109.6.76)  18.197 ms
    bu-ether25.nycmny837aw-bcr00.tbone.rr.com (107.14.19.22)  20.730 ms  16.201 ms
 6  0.ae0.pr1.nyc20.tbone.rr.com (107.14.17.216)  12.508 ms
    ge-2-1-3.a0.cle00.tbone.rr.com (66.109.1.57)  18.092 ms
    66.109.1.59 (66.109.1.59)  18.306 ms
 7  v1101.core1.nyc4.he.net (209.51.175.37)  17.945 ms  17.067 ms  22.374 ms
 8  100ge9-1.core2.chi1.he.net (184.105.223.161)  43.236 ms
    100ge16-1.core1.ash1.he.net (184.105.223.165)  21.576 ms  19.348 ms
 9  100ge2-2.core1.mci3.he.net (184.105.81.209)  46.955 ms
    100ge8-2.core1.mci3.he.net (184.105.222.77)  48.351 ms
    100ge14-2.core1.mci3.he.net (72.52.92.54)  48.822 ms
10  wholesale-internet-inc.10gigabitethernet1-3.core1.mci2.he.net (216.66.78.90)  51.545 ms  47.022 ms  47.746 ms
11  agge5-2.edge-b.clay.mci.us.as33387.net (69.30.209.218)  43.115 ms  49.859 ms  41.052 ms
12  agg-a.dist-2-2-a.clay.mci.us.as33387.net (192.187.107.25)  43.440 ms  42.648 ms  41.724 ms
13  onliare.com (204.12.214.178)  46.359 ms  49.177 ms  60.840 ms
```
