+++
title = "Shodan Stories Day 85: Hosting on Raspberry Pis in Arnstadt, CNAME Record Trails, and 'Home' Automation"
date = 2019-04-04T21:43:37-04:00
draft = false
tags = []
categories = ["100 days"]
+++

There's been a flurry of interesting recently shared searches on Shodan recently and I'm just catching up with them. Today I looked into one for [Raspberry Pis](https://www.raspberrypi.org/) running SSH that was just "port:22 "raspbian"". There are almost 100,000 results which I think goes to show just how popular these tiny computers are.

## A Raspberry Pi on 178.12.106.221
I picked a result in Germany because I saw that in addition to SSH it was also running a webserver on 443. All that webserver was hosting though was the word "home".
![](/images/100Days/Day85/firstlook.png)
The SSL certificate though had a bit more information.
![](/images/100Days/Day85/ssl.png)
home.jedemenge-it.de does indeed resolve to our IP address. jedemenge-it.de is entirely different however, so I think that the home. is a [CNAME](https://www.pickaweb.co.uk/kb/cname-can-use-domain/).
```
👻🌵🔮 $ host jedemenge-it.de
jedemenge-it.de has address 95.143.172.176
jedemenge-it.de mail is handled by 1 lupus.uberspace.de.
```
jedemenge-it.de itself is someone's personal website, almost certainly the owner of the Pi.

![](/images/100Days/Day85/website.png)
Looks like they do freelance web development and design. Pretty fun. And they are hosted by a company called UBER SPACE, which might be the best/worst webhost name I've seen.

See you tomorrow.
