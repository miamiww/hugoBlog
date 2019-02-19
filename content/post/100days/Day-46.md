+++
title = "Shodan Stories Day 46: Getting Connected in Vietnam, GPON ONT, VNPT, and the Mysteries of DNS Addressing"
date = 2019-02-18T10:37:03-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Someone was really looking for GPONs today, as I saw at least three searches for GPON related devices. What's a GPON you wonder? Let's find out together.

## VNPT GPON ONT on 14.161.15.80
GPON stands for [Gigabit Passive Optical Network](https://www.multicominc.com/solutions/technologies/gpon/). Though the real details of how they work escape me, it seems that they are a commonly used device by ISPs to separate out cable traffic between customers, frequently referred to as the "last mile" between the ISP and the end customer. If you could follow your internet line out of your apartment you'd might find that it attaches to one of these. They look like beefier home routers. I picked the first result I found on Shodan, this one from Vietnam.
![](/images/100Days/Day46/firstlook.png)
It was running a web login on port 80. The title of the login page indicated that it was a GPON ONT, ONT standing for Optical Network Terminal, which I think means its a device to login to a GPON, again the descriptions online were deeply technical and assumed a lot of knowledge that I don't have. It was also running a telnet server on 23, and interestingly a DNS server on 53. That makes sense if it has to figure out where to send traffic. I decided to check `host`.

```
➜  ~ host 14.161.15.80
80.15.161.14.in-addr.arpa domain name pointer static.vnpt.vn.
```
static.vnpt.vn, interestingly, does not follow back to the IP.
```
➜  ~ host static.vnpt.vn
static.vnpt.vn has address 203.162.0.78
```

[VNPT](https://en.wikipedia.org/wiki/VNPT) is the second biggest company in Vietnam, a government-owned telecom giant that services the country. Again it makes sense that an ISP is running this GPON.
![](/images/100Days/Day46/vnptb.png)
I have a hunch that VNPT has just given static.vnpt.vn to all of its static IPs that it wants to keep track of, which would explain why I can't get back to the original IP address from the url.

I at least half confirmed this with `traceroute`. As you can see the last six IPs are all under static.vnpt.vn

```
➜  ~ traceroute 14.161.15.80
traceroute to 14.161.15.80 (14.161.15.80), 64 hops max, 52 byte packets
 1  104.156.210.168 (104.156.210.168)  17.293 ms  21.589 ms  16.476 ms
 2  104.156.210.145 (104.156.210.145)  25.862 ms  20.676 ms  14.890 ms
 3  be5032.rcr24.jfk01.atlas.cogentco.com (38.140.161.137)  21.255 ms  18.065 ms  19.201 ms
 4  be2897.ccr42.jfk02.atlas.cogentco.com (154.54.84.213)  8.790 ms  32.817 ms  16.971 ms
 5  be3496.ccr31.jfk10.atlas.cogentco.com (154.54.0.142)  21.532 ms  23.978 ms  16.530 ms
 6  sprint.jfk10.atlas.cogentco.com (154.54.12.22)  18.141 ms  19.024 ms  16.820 ms
 7  144.232.25.231 (144.232.25.231)  30.889 ms  25.545 ms  43.399 ms
 8  144.232.14.7 (144.232.14.7)  24.993 ms  26.360 ms  23.946 ms
 9  144.232.13.195 (144.232.13.195)  41.530 ms  46.226 ms
    144.232.15.19 (144.232.15.19)  45.781 ms
10  144.232.22.142 (144.232.22.142)  59.395 ms  65.012 ms  75.958 ms
11  144.232.13.83 (144.232.13.83)  94.575 ms  104.589 ms
    144.232.22.229 (144.232.22.229)  71.012 ms
12  144.232.13.83 (144.232.13.83)  88.236 ms  79.454 ms
    144.232.22.163 (144.232.22.163)  84.890 ms
13  sl-vnpti-936487-0.sprintlink.net (144.223.54.186)  248.406 ms  257.803 ms
    144.232.22.163 (144.232.22.163)  92.586 ms
14  static.vnpt.vn (113.171.44.114)  283.990 ms  252.060 ms  314.919 ms
15  static.vnpt.vn (113.171.44.106)  260.108 ms
    static.vnpt.vn (113.171.48.142)  306.117 ms
    static.vnpt.vn (113.171.7.34)  305.441 ms
16  * static.vnpt.vn (113.171.48.218)  346.234 ms *
17  static.vnpt.vn (14.161.15.80)  258.466 ms * *
```

I tried to figure out what the device looked like. I went around on their website for awhile before ending up on [this page](http://www.vnpt-technology.vn/ViewDetailContentAction?categoryId=56&contentId=304).
![](/images/100Days/Day46/vnpta.png)
If you take a very close look at the bottom right of that image, you'll see that it is discussing GPONs. Let's take a closer look of the image of that device.
![](/images/100Days/Day46/GW240.png)
Yes! It's called an iGate, model GW240, with the words "GPON Optical Network Terminal" written on its side.

Like I said, beefier router. See you tomorrow.
