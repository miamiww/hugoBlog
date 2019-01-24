+++
title = "Shodan Stories Day 20: υηκηοωη ιδεηեτγ in France, Private Telephone Exchanges, Network Attached Storage, and Getting Lost in the Matrix"
date = 2019-01-23T12:45:18-08:00
draft = false
tags = []
categories = ["100 days"]
+++

Oh what a tangled web we weave. I'm not really sure what's going on with this one or how I got here, I wanted to explore a search I had seen on Shodan called "3cx servers bcn" but now I'm trapped in a digital hall of mirrors. [3CX](https://en.wikipedia.org/wiki/3CX_Phone_System) is a private telephone exchange that sometimes runs over [VoIP](https://en.wikipedia.org/wiki/Voice_over_IP), and has servers that typically tend to run on 5001.

## υηκηοωη ιδεηեτγ on 62.23.216.99
So I looked for things running on ports 5001. One of the first ones I saw was named "υηκηοωη ιδεηեτγ" which, naturally, got me pretty interested.
![](/images/100Days/Day20/ssl.png)
Going to their IP in a browser automatically tried for https but had a certificate error, and I was really struck by the url for which their certificate had been issued, which is to say that nyc-212.odin.biz sounds fake as hell. Thanks to Azalea Banks I know that 212 is an area code for NYC so at least that checked out with the phone theme. Let's come back to odin.biz in a bit.

Proceeding along to the IP prompts a login for υηκηοωη ιδεηեτγ. The login page is very pretty, there is a beach and some birds in the foreground and some mountains in the background. Again, we'll come back to this page later.
![](/images/100Days/Day20/unknown.png)
The login looked so nice I suspected that it must have a URL.
```
👻🌵🔮 $ host 62.23.216.99
99.216.23.62.in-addr.arpa domain name pointer mail.mx.vu.
```
Aha mail.mx.vu! So this is doing email or something related. What's mx.vu? It doesn't resolve to anything in the browser. According to Shodan it's in Garden City, Kansas.
```
👻🌵🔮 $ host mx.vu
mx.vu has address 209.200.39.39
mx.vu mail is handled by 10 mail.mx.vu.
mx.vu mail is handled by 20 syno.hno3.de.
👻🌵🔮 $ host syno.hno3.de
syno.hno3.de has address 89.246.70.219
👻🌵🔮 $ host hno3.de
hno3.de has address 80.237.132.25
hno3.de mail is handled by 50 mx0.hno3.de.
👻🌵🔮 $ host mx0.hno3.de
mx0.hno3.de has address 89.246.70.219
```
syno.hno3.de and hno3.de are both in Germany, unsurprisingly.
First hno3.de. It's running a page that just shows the following.
![](/images/100Days/Day20/hno3.png)

We'll get back to that one. Loose threads feel like they are piling up yet? Feel like there is a lot of υηκηοωη ιδεηեτγ still to be explored? syno.hno3.de is running on 443 with the following webpage:
![](/images/100Days/Day20/syno.png)
Just giving a 403 error. Usually that comes after a failed login meaning that you didn't have the correct credentials, and I was wondering if this page were looking for a specific IP to interact with it. I went looking for such a thing and found what was checking whether or not to give the error, a long javascript function embedded in the page that was determining whether or not to send the 403. It began like this:
```
/* Copyright (c) 2018 Synology Inc. All rights reserved. */

(function(){var a=new XMLHttpRequest();a.open("get","/missing",true); ...
```
Synology Inc! Major clue. And that page requires a specific request to be made via the url, which I was /missing. [Synology makes network attached storage](https://en.wikipedia.org/wiki/Synology_Inc.) as well as a router and a couple of other network goodies.
![](/images/100Days/Day20/server.png)
Now let's get back to the υηκηοωη ιδεηեτγ login. That page had a fair amount of javascript in it for a simple login page, much of it copyright Synology Inc.
![](/images/100Days/Day20/copyright.png)
There was also some from other companies, but they seemed to be doing web services and web design work, so it had likely been contracted out by Synology.
![](/images/100Days/Day20/lots.png)
So this login is probably for another Synology device, maybe storing mail.

But let's get back to odin.biz shall we?
```
👻🌵🔮 $ host nyc-212.odin.biz
nyc-212.odin.biz has address 62.23.216.99
```
That's the same IP that I had originally found. So mail.mx.vu is nyc-212.odin.biz. odin.biz however is considerably different from mx.vu. mx.vu doesn't appear to be hosting any web page of any kind, while odin.biz is hosting the same kind of thing as hno3.de!!
![](/images/100Days/Day20/odinbiz.png)
It turns out this is the default page for any server set up with [Host Europe GmbH](https://www.hosteurope.de/en/), which is the host for these pages. So someone set up these servers and parked default servers on the domain names and are using the domains to direct to a bunch of other servers via [CNAME](https://ns1.com/knowledgebase/comparing-alias-and-cname-records), some of which overlap. How deep does this go?

```
👻🌵🔮 $ host odin.biz
odin.biz has address 80.237.132.105
odin.biz mail is handled by 50 mx0.odin.biz.
👻🌵🔮 $ host mx0.odin.biz
mx0.odin.biz has address 80.237.138.5
👻🌵🔮 $ host  80.237.138.5
5.138.237.80.in-addr.arpa domain name pointer mx0.webpack.hosteurope.de.
👻🌵🔮 $ nmap odin.biz
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-23 23:41 EST
Nmap scan report for odin.biz (80.237.132.105)
Host is up (0.12s latency).
Other addresses for odin.biz (not scanned): 2a01:488:42:1000:50ed:8469:27:5029
rDNS record for 80.237.132.105: wp098.webpack.hosteurope.de
Not shown: 987 closed ports
PORT     STATE    SERVICE
21/tcp   open     ftp
22/tcp   open     ssh
25/tcp   open     smtp
80/tcp   open     http
110/tcp  open     pop3
143/tcp  open     imap
465/tcp  open     smtps
587/tcp  open     submission
993/tcp  open     imaps
995/tcp  open     pop3s
3306/tcp open     mysql
5666/tcp filtered nrpe
7000/tcp filtered afs3-fileserver
```


Too deep. υηκηοωη ιδεηեτγ remains as such. See you tomorrow.


PS another fun airplane traceroute today.
```
➜  ~ traceroute 62.23.216.99
traceroute to 62.23.216.99 (62.23.216.99), 64 hops max, 52 byte packets
 1  172.19.0.1 (172.19.0.1)  9.824 ms  2.049 ms  2.665 ms
 2  * * *
 3  * * *
 4  * * *
 5  192.168.142.2 (192.168.142.2)  725.002 ms  624.450 ms  600.828 ms
 6  * * *
 7  * * *
 8  * * *
 9  * * *
10  * * *
11  * * *
12  * * *
13  * * *
14  ae-2-3209.edge5.paris1.level3.net (4.69.143.170)  918.353 ms  835.658 ms  865.845 ms
15  colt-teleco.edge5.paris1.level3.net (212.73.200.90)  817.856 ms  822.151 ms  776.249 ms
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  * * *
29  * * *
30  * * *
31  * * *
32  * * *
```
