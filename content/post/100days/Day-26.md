+++
title = "Shodan Stories Day 26: Multicasting in Siberia, UDP Packet Pixies, and Free Civ"
date = 2019-01-29T22:22:18-05:00
draft = false
tags = []
categories = ["100 days"]
+++

The other day I saw someone on Shodan searching for "udpxy", and I couldn't determine what was going on with that because all of the results would give me 401 no auth errors. Today I realized that I could, of course, add "200 OK" to the search and only return successful connections. So I did.


## A Udpxy Server on 5.136.117.163
There were only two results, both in Russia, so I picked the one that seemed a little more interesting, from Tomsk, Siberia. I could see from Shodan that the "udpxy" service was running on port 4321, so I visited in a browser.
![](/images/100Days/Day26/udpxy.png)
[udpxy, pronounced "you-dee-pixie"](http://www.udpxy.com/), is a relay for multicast data streams to any HTTP clients that make the correct GET request. That means essentially that it can take multiple UDP streams and turn them into something accessible over HTTP. You might want to do this so that you can [pipe your captured cable tv streams to your smart phone](https://angrytechnician.wordpress.com/2012/07/31/converting-your-multicast-iptv-freeview-to-http-unicast-using-udpxy/), or something like that. In everything I could read about this application however it seemed to be for running on your local network first and foremost, with most long-term internet applications having better and safer tools available, which would explain why there were only two results on Shodan that were accessible. So I got kind of curious about why this one, and did a port scan.
```
👻 🌵 ✨ $ nmap 5.136.117.163
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-29 17:49 EST
Nmap scan report for 5.136.117.163
Host is up (0.18s latency).
Not shown: 997 closed ports
PORT     STATE    SERVICE
53/tcp   open     domain
4321/tcp open     rwhois
5555/tcp filtered freeciv

Nmap done: 1 IP address (1 host up) scanned in 20.35 seconds
```
What's that on port 5555? Freeciv, as in Free [Civilization](https://en.wikipedia.org/wiki/Civilization_(series))? [The open source implementation of blockbuster game franchise Civilization]((http://www.freeciv.org/))? [Built in 1996 and still looks the same even though it's been in steady beta development for _23 years_](https://en.wikipedia.org/wiki/Freeciv)? I was a little suspicious, because ports are frequently used for things other than what the common label is for them, especially snappy all the same number ones like 5555. I found that it was closed to TCP connections but UDP was working! That would make sense if this were a Freeciv server, which would require real time gaming.
```
➜  sandbox git:(master) ✗ nc -vu  5.136.117.163 5555
found 0 associations
found 1 connections:
     1: flags=82<CONNECTED,PREFERRED>
        outif (null)
        src 192.168.0.108 port 50154
        dst 5.136.117.163 port 5555
        rank info not available

Connection to 5.136.117.163 port 5555 [udp/personal-agent] succeeded!
```
So I thought I'd install Freeciv and see if I could join their server.
![](/images/100Days/Day26/freeciv.png)
It's extremely quaint. I had to install and start it from the command line, brings me back to the golden age of MS-DOS gaming. Those were truly the days.

![](/images/100Days/Day26/freecivnet2.png)
Sure enough you can connect to a remote server. There were a couple that just showed up in my list. When I tried to connect to this server however I timed out, and then the game crashed.

Too bad. I looked into whether the multicasting could be related to the gaming. [It seems that... yes?](https://freeciv.fandom.com/wiki/Forum:Multicast_message_to_freeciv_serverS_runing_on_the_same_machine?t=20100205185257) The answer got a bit too in the weeds for me to figure out.
I have a new game to play anyway. See you tomorrow.
