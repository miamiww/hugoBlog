+++
title = "Shodan Stories Day 13: Space X Email Server in Tokyo, No Not That Space X"
date = 2019-01-16T14:37:54-05:00
draft = false
tags = []
categories = ["100 days"]
+++

In honor of my spending about six hours on an airplane today I decided to search Shodan for "satellite" and, giving myself over to fate, pick the first result without looking at it.

## The Email Server of a Long Defunct Conference at 163.44.163.77
Since I was inspired by the fact that my airplane is being [serviced by satellite internet](https://en.wikipedia.org/wiki/Viasat,_Inc.) I was of course hoping that I would find the IP for [a real actual space satellite](https://www.quora.com/Do-communication-satellites-have-ip-addresses-If-so-what-are-they), though I suspected I was more likely to find someone's [satellite internet router or satellite dish](https://www.dish.com/internet/). Needless to say my first check on this IP got me very excited.
```
👻🌵🔮 $ host 163.44.163.77
77.163.44.163.in-addr.arpa domain name pointer ip015.space-x-vie.net.
```
"Space X! They make satellites!" I think, [quickly starting to poke around as much as possible](https://www.alphr.com/space/1008632/Elon-Musk-SpaceX-Starlink-internet). Unexpectedly I found that every single port is opened, all 65000ish (note I later figured out this is because `nmap` was getting interfered with on the airline wifi - can't figure out how though). Seems unlikely for a satellite. They also appear to be in Tokyo, although I can't imagine a satellite would actually say it is in "space". So I tried going to and then port mapping space-x-vie.net but they didn't seem to exist, which is when I tried [Internet Archive](https://web.archive.org/web/20101201080921/http://www.space-x-vie.net:80/s).

![](/images/100Days/Day13/space-x2010.png)
Space-x Vienna was a conference in Vienna on design for the visually impaired that ran twice, in 2010 and 2013. It had a global scope and attendance but seemed to be hosted primarily by Japanese organizations. Their website went dark back in 2016, so why was there an IP associated with them still hanging around. And not just one.
```
👻🌵🔮 $ host ip014.space-x-vie.net
ip014.space-x-vie.net has address 163.44.163.76
ip014.space-x-vie.net mail is handled by 10 ip014.space-x-vie.net.
👻🌵🔮 $ host ip013.space-x-vie.net
ip013.space-x-vie.net has address 163.44.163.75
ip013.space-x-vie.net mail is handled by 10 ip013.space-x-vie.net.
👻🌵🔮 $ host ip012.space-x-vie.net
ip012.space-x-vie.net has address 163.44.163.74
ip012.space-x-vie.net mail is handled by 10 ip012.space-x-vie.net.
👻🌵🔮 $ host ip011.space-x-vie.net
ip011.space-x-vie.net has address 163.44.163.73
ip011.space-x-vie.net mail is handled by 10 ip011.space-x-vie.net.
👻🌵🔮 $ host ip010.space-x-vie.net
ip010.space-x-vie.net has address 163.44.163.72
ip010.space-x-vie.net mail is handled by 10 ip010.space-x-vie.net.
👻🌵🔮 $ host ip009.space-x-vie.net
ip009.space-x-vie.net has address 163.44.163.71
ip009.space-x-vie.net mail is handled by 10 ip009.space-x-vie.net.
👻🌵🔮 $ host ip008.space-x-vie.net
ip008.space-x-vie.net has address 163.44.163.70
ip008.space-x-vie.net mail is handled by 10 ip008.space-x-vie.net.
👻🌵🔮 $ host ip007.space-x-vie.net
ip007.space-x-vie.net has address 163.44.163.69
ip007.space-x-vie.net mail is handled by 10 ip007.space-x-vie.net.
```
It looks like they have 17 total still up and associated with them (all named ip001-ip017) and they are all running email servers, all with every port open. Why? And if the Space X thing was just a red herring for satellites, how did they show up in my search?

Acutally I was able to answer that second question. Since `host` indicates that they are all running email, I thought I'd check port 25, which is a frequently used SMTP port for email. Netcatting to that port gives the following result:
```
👻🌵🔮 $ nc 163.44.163.77 25
220 st014.satellite-mail.net ESMTP unknown
```
I checked every IP and they are all connected to st014.satellite-mail.net. What's that you might ask? A reasonable question.
```
👻🌵🔮 $ host st014.satellite-mail.net
st014.satellite-mail.net has address 150.95.138.218
st014.satellite-mail.net mail is handled by 10 st014.satellite-mail.net.
👻🌵🔮 $ host ip001.space-x-vie.net
ip001.space-x-vie.net has address 150.95.138.218
ip001.space-x-vie.net mail is handled by 10 ip001.space-x-vie.net.
```
It turns out it is ip001.space-x-vie.net! So it's 16 IPs doing email all off of the first IP, which is doing email off of itself. Maybe? Who knows anymore in this wacky messed up world. See you tomorrow.


PS if you want to see what a traceroute to Google looks like on an airplane I have got the goods for you.
```
👻🌵🔮 $ traceroute www.google.com
traceroute to www.google.com (172.217.12.68), 64 hops max, 52 byte packets
 1  172.19.0.1 (172.19.0.1)  2.044 ms  2.761 ms  2.889 ms
 2  * * *
 3  * * *
 4  * * *
 5  192.168.142.2 (192.168.142.2)  671.316 ms  684.715 ms  581.512 ms
 6  * * *
 7  * * *
 8  * * *
 9  * * *
10  * * *
11  * * *
12  206.53.175.23 (206.53.175.23)  633.117 ms  654.253 ms  681.984 ms
13  108.170.252.203 (108.170.252.203)  609.477 ms
    108.170.254.82 (108.170.254.82)  622.657 ms
    108.170.252.201 (108.170.252.201)  620.264 ms
14  172.253.51.80 (172.253.51.80)  710.279 ms
    172.253.51.116 (172.253.51.116)  717.226 ms
    172.253.51.118 (172.253.51.118)  614.161 ms
15  72.14.239.159 (72.14.239.159)  716.628 ms  619.877 ms  611.338 ms
16  216.239.63.206 (216.239.63.206)  982.626 ms  715.172 ms  718.053 ms
17  108.170.252.161 (108.170.252.161)  715.825 ms  613.966 ms  602.376 ms
18  108.170.226.109 (108.170.226.109)  683.573 ms  666.308 ms  608.380 ms
19  dfw28s05-in-f4.1e100.net (172.217.12.68)  623.938 ms  615.781 ms  718.200 ms
```

Here's the route to the IP in question just in case you were wondering.
```🌵🔮 $ traceroute 163.44.163.75
traceroute to 163.44.163.75 (163.44.163.75), 64 hops max, 52 byte packets
 1  172.19.0.1 (172.19.0.1)  8.436 ms  1.499 ms  2.258 ms
 2  * * 100.106.31.254 (100.106.31.254)  439.805 ms !H
 3  * * *
 4  * * *
 5  * * *
 6  * * *
 7  * * *
 8  * * *
 9  * * *
10  * * *
11  * * *
12  206.53.175.19 (206.53.175.19)  596.554 ms  686.772 ms  615.273 ms
13  100ge12-1.core1.lax2.he.net (184.105.222.113)  719.048 ms  645.211 ms  658.568 ms
14  softbank221111203065.bbtec.net (221.111.203.65)  858.888 ms  714.100 ms  764.370 ms
15  * * *
16  218.45.246.190 (218.45.246.190)  758.650 ms  824.528 ms  1076.217 ms
17  aha.37.s-port.biz (202.94.181.37)  1055.662 ms  836.070 ms  822.678 ms
18  * * *
19  c-5en-a11-2-v-712.interq.or.jp (157.7.41.130)  1065.874 ms  818.556 ms *
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
33  * * *
34  * * *
35  * * *
36  * * *
37  * * *
38  * * *
39  * * *
40  * * *
41  * * *
42  * * *
43  * * *
44  * * *
45  * * *
46  * * *
47  * * *
48  * * *
49  * * *
50  * * *
51  * * *
52  * * *
53  * * *
54  * * *
55  * * *
56  * * *
57  * * *
58  * * *
59  * * *
60  * * *
61  * * *
62  * * *
63  * * *
64  * * *
```
