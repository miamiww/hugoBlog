+++
title = "Shodan Stories Day 42: Party Mode in Kleppestø, Yamaha Receivers, "
date = 2019-02-14T22:41:11-05:00
draft = false
tags = []
categories = ["100 days"]
+++

I saw that someone was searching for quite a few different types of AV receivers today. I decided to look into one of their searches, this one for Yamaha receiver.
## Yamaha AV Recievers on 90.149.252.214
I'm not sure what the typical use-case for remote control of an AV receiver is. Maybe if you run a cafe and you want to make sure your untrustworthy employees don't make the music too loud while you're out? I'm sure it's incredibly useful in certain situations, but I can't think of any off the top of my head. All of the Yamaha ones were running a webserver off port 80, so I picked one in Norway and took a look.
![](/images/100Days/Day42/firstlook.png)
Amazing, I have complete control over the volume. I'm also capable of flipping the "PARTY MODE" switch, likely with dire consequences for the immediate surroundings of this device. I could also turn the device off, but that would probably also cut off my connection. There's also a settings button.
![](/images/100Days/Day42/settings.png)
Great, all the goodies. Probably the worst thing someone could do right off the bat is brick it, but if they had a malicious version of the firmware they could install that as well. Looks like this is a RX-A1030 model.
![](/images/100Days/Day42/discontinued.png)
Which is now discontinued. A hymn for those lost, firmware eternally waiting for the next upgrade, never to arrive. I found the user manual, trying to understand why someone would want a device with remote internet control, but it was 150 pages, and I've got like a life to live.

I did decide to give it an `nmap` to see if I could find anything else about it.
```
👻🌵🔮 $ nmap 90.149.252.214
Starting Nmap 7.70 ( https://nmap.org ) at 2019-02-14 22:40 EST
Nmap scan report for 214.90-149-252.nextgentel.com (90.149.252.214)
Host is up (0.12s latency).
Not shown: 995 closed ports
PORT      STATE SERVICE
80/tcp    open  http
1024/tcp  open  kdm
1900/tcp  open  upnp
8080/tcp  open  http-proxy
50000/tcp open  ibm-db2

Nmap done: 1 IP address (1 host up) scanned in 76.96 seconds
```
1024 is [Apple Airplay](https://www.apple.com/airplay/). That [UPnP is open is a little unnerving](https://www.varonis.com/blog/what-is-upnp/), and I couldn't find any reason why the receiver would need that service, though it seems that, [based on some forum posts I found](https://forum.kodi.tv/showthread.php?tid=199774), people configure it to talk over that port to connect to their media servers. Risky when you're putting that all over the internet! 50000 is a mystery, [probably not one worth solving](https://blog.webernetz.net/yamaha-r-n500-network-receiver-port-scan/).

Delightfully 8080 is a webserver running a single, beautiful page.
![](/images/100Days/Day42/presentationpage.png)
PRESENTATION PAGE. Completely blank other than that.

If only all websites were so well thought out. See you tomorrow.
