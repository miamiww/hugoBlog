+++
title = "Shodan Stories Day 63: Securities Trading in Hong Kong, Ghidra vs IDA Pro, and the Ever Popular Insecure Java Debugger"
date = 2019-03-07T21:20:35-05:00
draft = false
tags = []
categories = ["100 days"]
+++

There's been a lot of hubbub in the infosec world the past couple of days because the NSA released one of their reverse engineering tools, [Ghidra, as an open source toolkit](https://www.wired.com/story/nsa-ghidra-open-source-tool/). This is huge news because the closest tool in functionality, [IDA Pro](https://www.hex-rays.com/products/ida/), is $1200 a year for a license, but also raised a question: would you trust software from the NSA, even if it's hosted on Github?
![](/images/100Days/Day63/Ghidra.png)
I'm starting with this preamble because of a default setting in Ghidra. If you run the software in "debug mode", by default it starts running a server on port 18001 that allows anyone to make a [tcp connection and execute code remotely over the internet](https://www.zdnet.com/article/nsa-release-ghidra-a-free-software-reverse-engineering-toolkit/). Whoops?

## Global Mastermind Securities on 202.82.115.202
I ran a search on Shodan for anything running port 18001. Turns out that's a great way to find everything that has every port open running a service on every port, like the website I found on day 41. I looked through all 500 results and I'm not sure I found anyone who was running Ghidra insecurely. I was expecting to see a result that looked like a "[Java Debug Wire Protocol](https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/introclientissues005.html)" service, which is a Java debugger, but nothing with 18001 looked like it was doing a Java debugger. But I did find a few interesting things.

One of the IP addresses not running a mirrored service on every port was running a webserver on 80 and 443, and then the 18001 service. Both of the webservers gave 403 no authentication errors, but 443 did have an ssl certificate with a domain name attached.
![](/images/100Days/Day63/ssl.png)

Let's check that url real quick.
```
➜  ~ host trade.globalmsec.com
trade.globalmsec.com has address 202.82.115.239
```
It's not quite the IP address we are looking at, but it's close. Now checking all the nearby IPs, all the IP addresses between 202.82.115.193 and 202.82.115.235 are 403 forbiddens with ssl certificates set to names that sound like online trade platforms. Here's a list of a few of my favorites:

>www.onlinetrade.hss.com.hk

>online.gwfg.com.hk

>ayers.com.hk

>www.kuentaisec.com.hk

>etrade.shunloongsec.com

>etrade2.ccnew.com.hk

>etrade.conrad-is.com.hk

Now as far as I can tell these are all under the provenance of separate, distinct companies. So why are all of these financial trading services lumped together in the same IP range? I have no idea. Maybe they are all running out of the same server farm in the Hong Kong stock exchange.

Getting back to our original IP address, I checked out globalmsec.com
![](/images/100Days/Day63/globalmsec.png)
They seem like a lovely financial services company. Just look at that skyline! With a name like Global Mastermind, how can you not just give them all your investment capital? Now what really caught my attention though is the little "Online Trade Login" in the top right corner. So I clicked.
![](/images/100Days/Day63/trade.png)
Aha! The url I want. And now I know probably what I need to append to the IP address to get around the 403, all that /mts.web/ stuff.
![](/images/100Days/Day63/ip.png)
And there you go. Interestingly this doesn't work for 202.82.115.239, which instead claims to belong to ayers.com.hk.

So maybe there is a conspiracy after all. See you tomorrow.
