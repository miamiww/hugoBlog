+++
title = "Shodan Stories Day 64: Pro DJing in Antofagasta, Iomega NAS, and a Torrenting Minimalist"
date = 2019-03-08T22:55:18-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I saw a search for [Iomega (now Lenovo EMC)](https://en.wikipedia.org/wiki/LenovoEMC) Network Attached Storage, probably because [these devices have been show to have huge security flaws](https://support.lenovo.com/us/en/solutions/len-24224) (or the novelty of finding devices that still have "Iomega" written into their cookie code even after the brand had been incorporated into Lenovo). But I thought it would be a nice change from all of the Synology NAS we've been seeing.

## Lenovo EMC NAS on 190.161.190.19
I picked a result in Chile, but looked at quite a few results before picking this one. They all are running webservers on 443 and they all look exactly like this.
![](/images/100Days/Day64/firstlook.png)
Yes they all of these same three images! The three ideal landscapes, I guess. I really want to know who at Iomega (now LenovoEMC) made the design choice to include a little three image slideshow in every device. And then who picked out the images?
![](/images/100Days/Day64/torrent.png)
What got my attention was that this NAS was sharing a single folder just called "Torrent", which, I think it is pretty safe to assume refers to bittorenting.
![](/images/100Days/Day64/files.png)
Let's take a peak inside. It's someone using a mac because they have .DS_Store (and .AppleDesktop). All of the folders are empty, except for DOWNLOAD.
![](/images/100Days/Day64/djaypro.png)
Amazingly it looks like all they have been torrenting is the same DJ software over and over again. They first downloaded it November of 2018 and have either been making a copy every couple of weeks since then or have been downloading it multiple times. It doesn't really make sense. Where's the 30GB of FLAC music? The porn? The James Cameron's Avatar blueray rips?
![](/images/100Days/Day64/djay.png)
DJay Pro is also bad and [gimmicky](https://www.theverge.com/2017/12/12/16764040/djay-pro-2-software-ai-automix-algoriddim). I don't get it.

Just to confirm that this is still torrenting I thought I'd check the typical bittorrent port, 6881.
```
👻🌵🔮 $ nmap -A -p 6881 190.161.190.19
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-08 23:34 EST
Nmap scan report for pc-19-190-161-190.cm.vtr.net (190.161.190.19)
Host is up (0.0012s latency).

PORT     STATE    SERVICE            VERSION
6881/tcp filtered bittorrent-tracker

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.58 seconds

👻🌵🔮 $ nc -v 190.161.190.19 6881
found 0 associations
found 1 connections:
     1: flags=82<CONNECTED,PREFERRED>
        outif ipsec0
        src 10.6.6.83 port 57027
        dst 190.161.190.19 port 6881
        rank info not available
        TCP aux info available

Connection to 190.161.190.19 port 6881 [tcp/*] succeeded!
^C
```
Yup it's still running! I wonder how many GB of DJay Pro 2 they've uploaded. See you tomorrow.
