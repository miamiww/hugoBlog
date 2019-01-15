+++
title = "Day 11"
date = 2019-01-14T14:27:56-05:00
draft = false
tags = []
categories = ["100 days"]
+++
Today I went looking for [MongoDB](https://www.mongodb.com/) databases. I used MongoDB back in Shawn Van Every's servers class, I remember feeling pretty cool using a [NoSQL database](https://en.wikipedia.org/wiki/NoSQL). Shodan indicated that MongoDB tends to work off of port 27017 so that's where I started looking.

## The Shell of Someone's Machine Learning Blog on 35.185.145.24
I picked one of the first results I found on Shodan. According to Shodan it's located in Singapore and hosted on Google Cloud services. After running `nmap` on the IP I saw it had port 80, the http port, open so I decided to visit it in a browser.
```
➜  sandbox git:(master) ✗ nmap -p- 35.185.145.24
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-14 18:02 EST
Nmap scan report for 24.145.185.35.bc.googleusercontent.com (35.185.145.24)
Host is up (0.21s latency).
Not shown: 65528 closed ports
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
3010/tcp  open  gw
8080/tcp  open  http-proxy
8088/tcp  open  radan-http
8989/tcp  open  sunwebadmins
27017/tcp open  mongod

Nmap done: 1 IP address (1 host up) scanned in 1507.34 seconds
```
![](/images/100Days/Day11/ailab.png)
It looks like a blog named AI Lab with a bunch of posts about how to use quite an extensive range of machine learning tools. Additionally it has posts about songs and music. Some things are off though. None of the media embeddings work (i.e. none of the songs play), every post has 666 likes and no comments, some of the code formatting is broken and unreadable in the posts, and quite a few of the image links are broken. Also it has no DNS entry, it's only resolving to the googleusercontent.com URL. Clearly this blog is not meant for public eyes. The bottom has a note about the author: their name is Leo, and you can message them on WeChat.
![](/images/100Days/Day11/wechat.png)
So now I really wanted to know about the history of this blog and I got kind of overly obsessed with why it's in this quasi state of reality. I thought about messaging Leo, but I thought that would be too weird right off the bat, though I did check Leo's WeChat page and it said that they were in Beijing, not Singapore. That makes sense for two reasons: the website is in simplified Chinese, and not traditional like they use in Singapore, and Google doesn't have facilities in China to my knowledge so if you want to use Google hosting and you're in Beijing then Singapore seems like a close option.

There's a signup and login (?) at the top right I thought about trying to join but decided that that would be too weird also. I tried probing all the other open ports and one of them yielded returns, 8080, which seems to be hosting an entirely different, though related, website.
![](/images/100Days/Day11/wiki.png)
This is kind of like a documentation website that goes through many specific tools than in the blog, which does more deep dives on things like processes and methodologies.
```
➜  1Semester git:(master) ✗ traceroute 24.145.185.35.bc.googleusercontent.com
traceroute to 24.145.185.35.bc.googleusercontent.com (35.185.145.24), 64 hops max, 52 byte packets
 1  192.168.0.1 (192.168.0.1)  1.379 ms  1.358 ms  1.047 ms
 2  * * *
 3  be61.nycynymy01h.nyc.rr.com (68.173.202.72)  14.620 ms  11.265 ms  14.465 ms
 4  agg113.nyclnyrg01r.nyc.rr.com (68.173.198.40)  16.134 ms  19.683 ms  14.992 ms
 5  bu-ether29.nwrknjmd67w-bcr00.tbone.rr.com (107.14.19.24)  20.367 ms  8.660 ms  15.925 ms
 6  66.109.5.138 (66.109.5.138)  18.707 ms
    bu-ether12.nycmny837aw-bcr00.tbone.rr.com (66.109.6.27)  19.087 ms
    66.109.5.138 (66.109.5.138)  17.919 ms
 7  0.ae4.pr0.nyc20.tbone.rr.com (66.109.1.35)  12.444 ms
    0.ae0.pr0.nyc20.tbone.rr.com (66.109.6.157)  15.421 ms
    0.ae4.pr0.nyc20.tbone.rr.com (66.109.1.35)  19.376 ms
 8  ix-ae-10-0.tcore1.n75-new-york.as6453.net (66.110.96.13)  9.780 ms  11.807 ms
    ix-ae-6-0.tcore1.n75-new-york.as6453.net (66.110.96.53)  21.147 ms
 9  72.14.195.232 (72.14.195.232)  15.867 ms  14.708 ms  13.809 ms
10  74.125.251.231 (74.125.251.231)  15.645 ms  39.872 ms
    74.125.251.227 (74.125.251.227)  11.423 ms
11  108.170.248.20 (108.170.248.20)  16.561 ms
    108.170.248.99 (108.170.248.99)  14.053 ms
    108.170.248.20 (108.170.248.20)  27.425 ms
12  108.170.226.123 (108.170.226.123)  13.607 ms
    209.85.255.27 (209.85.255.27)  12.391 ms
    209.85.254.139 (209.85.254.139)  12.974 ms
13  216.239.58.254 (216.239.58.254)  33.820 ms
    216.239.57.136 (216.239.57.136)  36.191 ms
    216.239.57.196 (216.239.57.196)  53.178 ms
14  209.85.241.43 (209.85.241.43)  100.000 ms  113.480 ms
    72.14.239.209 (72.14.239.209)  117.318 ms
15  72.14.239.30 (72.14.239.30)  93.174 ms
    66.249.94.92 (66.249.94.92)  93.079 ms
    72.14.239.155 (72.14.239.155)  99.012 ms
16  108.170.234.21 (108.170.234.21)  220.932 ms
    209.85.249.41 (209.85.249.41)  206.196 ms
    108.170.234.21 (108.170.234.21)  206.989 ms
17  209.85.245.48 (209.85.245.48)  203.529 ms
    72.14.233.35 (72.14.233.35)  214.472 ms
    66.249.95.76 (66.249.95.76)  204.603 ms
18  216.239.40.29 (216.239.40.29)  211.199 ms
    74.125.252.245 (74.125.252.245)  198.960 ms  222.302 ms
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  24.145.185.35.bc.googleusercontent.com (35.185.145.24)  201.603 ms  206.988 ms  207.457 ms
```

```
Domain Name: riverrun.cn
ROID: 20140703s10001s71703193-cn
Domain Status: ok
Registrant ID: 6681981404378845
Registrant: 侯光敏
Registrant Contact Email: guangmin001@163.com
Sponsoring Registrar: 成都飞数科技有限公司
Name Server: f1g1ns1.dnspod.net
Name Server: f1g1ns2.dnspod.net
Registration Time: 2014-07-03 17:14:08
Expiration Time: 2019-07-03 17:14:08
DNSSEC: unsigned
```

```
Domain Name: 163.com
Registry Domain ID: 473619_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.markmonitor.com
Registrar URL: http://www.markmonitor.com
Updated Date: 2018-08-13T02:16:31-0700
Creation Date: 1997-09-14T21:00:00-0700
Registrar Registration Expiration Date: 2020-09-13T00:00:00-0700
Registrar: MarkMonitor, Inc.
Registrar IANA ID: 292
Registrar Abuse Contact Email: abusecomplaints@markmonitor.com
Registrar Abuse Contact Phone: +1.2083895740
Domain Status: clientUpdateProhibited (https://www.icann.org/epp#clientUpdateProhibited)
Domain Status: clientTransferProhibited (https://www.icann.org/epp#clientTransferProhibited)
Domain Status: clientDeleteProhibited (https://www.icann.org/epp#clientDeleteProhibited)
Domain Status: serverUpdateProhibited (https://www.icann.org/epp#serverUpdateProhibited)
Domain Status: serverTransferProhibited (https://www.icann.org/epp#serverTransferProhibited)
Domain Status: serverDeleteProhibited (https://www.icann.org/epp#serverDeleteProhibited)
Registrant Organization: Guangzhou NetEase Computer System Co., Ltd
Registrant State/Province: Guangdong
Registrant Country: CN
Admin Organization: Guangzhou NetEase Computer System Co., Ltd
Admin State/Province: Guangdong
Admin Country: CN
Tech Organization: Guangzhou NetEase Computer System Co., Ltd
Tech State/Province: Guangdong
Tech Country: CN
Name Server: ns4.nease.net
Name Server: ns3.nease.net
Name Server: ns6.nease.net
Name Server: ns1.nease.net
Name Server: ns2.166.com
Name Server: ns8.166.com
Name Server: ns5.nease.net
DNSSEC: unsigned
URL of the ICANN WHOIS Data Problem Reporting System: http://wdprs.internic.net/
>>> Last update of WHOIS database: 2019-01-14T16:40:25-0800 <<<
```

```
➜  sandbox git:(master) ✗ host 163.com
163.com has address 123.58.180.8
163.com has address 123.58.180.7
163.com mail is handled by 10 163mx02.mxmail.netease.com.
163.com mail is handled by 10 163mx03.mxmail.netease.com.
163.com mail is handled by 50 163mx00.mxmail.netease.com.
163.com mail is handled by 10 163mx01.mxmail.netease.com.
```

```
➜  sandbox git:(master) ✗ host music.163.com
music.163.com has address 103.65.41.125
music.163.com has address 103.65.41.126
```

```
➜  sandbox git:(master) ✗ host 163yun.com
163yun.com has address 59.111.163.236
163yun.com mail is handled by 5 hzmx01.mxmail.netease.com.
163yun.com mail is handled by 10 hzmx02.mxmail.netease.com.
```

[Finally I figured it out, sort of.](https://www.quora.com/What-does-126-and-163-mean-in-Chinese-language)
