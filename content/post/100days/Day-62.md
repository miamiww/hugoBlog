+++
title = "Shodan Stories Day 62: Night at the Kino in Winnenden"
date = 2019-03-06T21:17:39-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I wanted to find a webcam but not because I needed an easy target, but rather so that I could find a webcam that would lead me to its precise location. I mulled about in Shodan's image viewer until I found an interesting result, and lo and behold, it's another webcam server made by Steven Wu (see days 38 and 47 if that name doesn't ring a bell). Thank you, Steven Wu, for your really terribly insecure webcam server.

## A Kino on 87.128.13.137
The result I picked was both appealing for what I saw through the webcam, but also for its Shodan-given location: [Winnenden, Germany](https://en.wikipedia.org/wiki/Winnenden), a tiny town of 28,000. Now, for what I saw through the webcam.
![](/images/100Days/Day62/lobby.jpg)
Sure looks like a move theater lobby right? Now in a 28,000 person town, there couldn't be too many movie theaters right? Turns out that in Winnenden, there's only one, Olympia Kino (kino is German for movie theater).
![](/images/100Days/Day62/olympia.png)
IP address location services are notoriously inaccurate, however, so how could I be sure that this was the one? I decided to give the IP address an `nmap` to see if I could get any info.

```
➜  sandbox git:(master) ✗ nmap 87.128.13.137
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-06 22:32 EST
Nmap scan report for p57800d89.dip0.t-ipconnect.de (87.128.13.137)
Host is up (0.15s latency).
Not shown: 934 closed ports, 59 filtered ports
PORT     STATE SERVICE
22/tcp   open  ssh
81/tcp   open  hosts2-ns
82/tcp   open  xfer
83/tcp   open  mit-ml-dev
85/tcp   open  mit-ml-dev
443/tcp  open  https
5900/tcp open  vnc

Nmap done: 1 IP address (1 host up) scanned in 606.43 seconds
```
The webcam I was originally looking at was on port 82, so I decided to look at 81.
![](/images/100Days/Day62/closet.png)
Another one of Steven Wu's finest, this time of what must be the building's electrical closet. Why put a webcam here? Maybe to monitor the knobs? Make sure they aren't turning themselves?

I was hoping 83 and 85 were webcams as well, but they were garden variety authentication logins. 443 had a less garden-variety login.
![](/images/100Days/Day62/lancom.png)
The router! Now as we all know the Lancom 1781VAW is [the ideal choice for small and medium-sized businesses needing VPN networking and wireless connections for mobile clients](https://www.lancom-systems.com/products/routers-vpn-gateways/business-vpn-routers/lancom-1781vaw/). I'm not sure why they would need VPN networking, but they might have just chosen this router because Lancom seems to have [considerable market share for business routers in Germany](https://wifinowevents.com/news-and-blog/leading-german-wi-fi-vendor-lancom-acquired-by-rohde-schwartz/).

That leaves the VNC server, but unfortunately for me their VNC server is not wide open like the one I found all the way back on day 1.
![](/images/100Days/Day62/vnc.png)
Out of options on the network, I tried looking for images of the kino on social media to see if any matched up to the lobby view I was getting. I did find one picture of the Olympia Kino lobby.
![](/images/100Days/Day62/lobby2.png)
Doesn't look a whole lot like the lobby I'm seeing in the webcam, the floor is quite different and the door setup is different as well. I do see some [club mates](https://en.wikipedia.org/wiki/Club-Mate) in the fridge.

For awhile I started looking around at all the movie theaters in nearby towns, but once I got through about a half dozen I decided it was a fool's errand. I may never know for sure what movie theater this was, and I just have to live with that. See you tomorrow.
