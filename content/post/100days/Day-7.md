+++
title = "Day 7: Scammers in the Czech Republic, Cyrillic TLDs, and Hacking the Hackers"
date = 2019-01-10T15:19:23-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Someone tried to phish me yesterday via text from a Los Vegas phone number. Fortunately I was able to figure out their IP address and, yes, their IP is on Shodan.
![](/images/100Days/Day7/Phisher.png)
### Someone Trying to Phish Me on 146.120.89.201

I started out checking both номе.рф and xn--e1ance.xn--p1ai, which is the address the text message actually links to. In case you are wondering, and don't want to read further, номе.рф is save to go to but xn--e1ance.xn--p1ai is definitely not. Possibly because .рф and xn--p1ai seem like [rare top level domains](https://cctld.ru/en/), `nslookup` and `whois` didn't give me very interesting results. Apparently .xn--p1ai is an "administrative group" of .рф

```
👻🌵✨$ whois xn--e1ance.xn--p1ai
% IANA WHOIS server
% for more information on IANA, visit http://www.iana.org
% This query returned 1 object

refer:        whois.tcinet.ru

domain:       рф
domain-ace:   XN--P1AI

organisation: Coordination Center for TLD RU
address:      8 Marta street 1, bld 12
address:      Moscow  127083
address:      Russian Federation

contact:      administrative
name:         .xn--p1ai domain Administrative group
organisation: Coordination Center for TLD RU
address:      8 Marta street 1, bld 12
address:      Moscow  127083
address:      Russian Federation
phone:        +7 495 730 29 71
fax-no:       +7 495 730 29 68
e-mail:       ru-adm@cctld.ru

contact:      technical
name:         Technical Center of Internet
organisation: Technical Center of Internet
address:      8 Marta street 1, bld 12
address:      Moscow  127083
address:      Russian Federation
phone:        +7 495 730 29 69
fax-no:       +7 495 730 29 68
e-mail:       ru-tech@tcinet.ru

nserver:      A.DNS.RIPN.NET 193.232.128.6 2001:678:17:0:193:232:128:6
nserver:      B.DNS.RIPN.NET 194.85.252.62 2001:678:16:0:194:85:252:62
nserver:      D.DNS.RIPN.NET 194.190.124.17 2001:678:18:0:194:190:124:17
nserver:      E.DNS.RIPN.NET 193.232.142.17 2001:678:15:0:193:232:142:17
nserver:      F.DNS.RIPN.NET 193.232.156.17 2001:678:14:0:193:232:156:17
ds-rdata:     14585 8 2 96BFDB14DED2592146F371ECCC301305D6908042C614DB32ED87EB7D61FA8639

whois:        whois.tcinet.ru

status:       ACTIVE
remarks:      Registration information: http://cctld.ru/en

created:      2010-05-12
changed:      2018-09-24
source:       IANA

% By submitting a query to RIPN's Whois Service
% you agree to abide by the following terms of use:
% http://www.ripn.net/about/servpol.html#3.2 (in Russian)
% http://www.ripn.net/about/en/servpol.html#3.2 (in English).

domain:        XN--E1ANCE.XN--P1AI
nserver:       ns1.host.ukrnames.com.
nserver:       ns2.host.ukrnames.com.
state:         REGISTERED, DELEGATED, UNVERIFIED
person:        Private Person
registrar:     REGTIME-RF
admin-contact: http://whois.webnames.ru/
created:       2018-12-01T21:51:03Z
paid-till:     2019-12-01T21:51:03Z
free-date:     2020-01-02
source:        TCI

Last updated on 2019-01-10T21:01:31Z

```
Oddly I found that they both traced to the same IP address, 146.120.89.201, with a hostname of hosting18.ukrnames.com

```
➜  ~ traceroute номе.рф
traceroute to xn--e1ance.xn--p1ai (146.120.89.201), 64 hops max, 52 byte packets
 1  10.17.0.2 (10.17.0.2)  2.449 ms  2.170 ms  2.905 ms
 2  nyugwa-new-vl902.net.nyu.edu (128.122.1.36)  3.163 ms  2.749 ms  2.719 ms
 3  ngfw-palo-vl1500.net.nyu.edu (192.168.184.228)  3.430 ms  3.860 ms  2.335 ms
 4  nyugwa-outside-ngfw-vl3080.net.nyu.edu (128.122.254.114)  3.515 ms  3.472 ms  3.301 ms
 5  nyunata-vl1000.net.nyu.edu (192.168.184.221)  3.641 ms  3.759 ms  3.862 ms
 6  nyugwa-vl1001.net.nyu.edu (192.76.177.202)  3.648 ms  3.584 ms  4.012 ms
 7  dmzgwb-ptp-nyugwa-vl3082.net.nyu.edu (128.122.254.111)  4.553 ms  3.974 ms  4.471 ms
 8  extgwb-ptp-dmzgwb.net.nyu.edu (128.122.254.70)  4.214 ms  3.900 ms  3.855 ms
 9  ix-xe-7-3-2-0.tcore2.nw8-new-york.as6453.net (64.86.62.13)  4.338 ms  3.025 ms  4.352 ms
10  if-ae-0-2.tcore1.nw8-new-york.as6453.net (209.58.75.217)  101.840 ms  100.571 ms  104.496 ms
11  if-ae-3-2.tcore1.n0v-new-york.as6453.net (216.6.90.72)  101.431 ms  101.857 ms  100.484 ms
12  if-ae-2-2.tcore2.n0v-new-york.as6453.net (216.6.90.22)  103.265 ms  100.811 ms  101.136 ms
13  if-ae-4-2.tcore2.l78-london.as6453.net (80.231.131.157)  101.201 ms  101.149 ms  101.890 ms
14  if-ae-14-2.tcore2.av2-amsterdam.as6453.net (80.231.131.161)  101.837 ms  99.955 ms  103.644 ms
15  if-ae-2-2.tcore1.av2-amsterdam.as6453.net (195.219.194.5)  101.624 ms  100.298 ms  102.170 ms
16  if-ae-21-2.thar1.w1t-warsaw.as6453.net (195.219.188.26)  101.721 ms  100.463 ms  101.543 ms
17  195.219.188.38 (195.219.188.38)  117.767 ms  116.471 ms  116.671 ms
18  kh-kv.ett.ua (80.93.127.142)  125.322 ms  123.608 ms  123.810 ms
19  maxnet.ett.ua (80.93.125.250)  125.603 ms  123.471 ms  126.480 ms
20  ukrnames.maxnet.ua (79.171.125.210)  124.083 ms  124.304 ms  124.063 ms
21  hn4-kh.ukrnames.com (146.120.89.200)  126.725 ms  125.446 ms  127.229 ms
22  hosting18.ukrnames.com (146.120.89.201)  123.240 ms  123.425 ms  124.552 ms
```
I'm sure that [ukrnames](https://www.ukrnames.com/) is totally legit and aboveboard as a web hosting service but I couldn't help being reminded of a conference talk I had been to by [Brannon Dorsey](https://radicalnetworks.org/archives/2017/participants/brannon-dorsey/) talking about how Ukranian hosting services were the only way to completely anonymously buy web hosting via crypto currencies. This IP [shows up on Shodan](https://www.shodan.io/host/146.120.89.201) being in the domain of [Alfa Telecom](http://alfatelecom.cz/) in the Czech Republic. Using `nmap` reveals that they've got a lot going on.

```
👻🌵✨$ nmap -p- 146.120.89.201
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-10 15:04 EST
Nmap scan report for hosting18.ukrnames.com (146.120.89.201)
Host is up (0.13s latency).
Not shown: 65509 closed ports
PORT      STATE    SERVICE
21/tcp    open     ftp
25/tcp    open     smtp
80/tcp    open     http
81/tcp    open     hosts2-ns
110/tcp   open     pop3
143/tcp   open     imap
443/tcp   open     https
465/tcp   open     smtps
587/tcp   open     submission
993/tcp   open     imaps
995/tcp   open     pop3s
2077/tcp  open     tsrmagt
2078/tcp  open     tpcsrvr
2079/tcp  open     idware-router
2080/tcp  open     autodesk-nlm
2082/tcp  open     infowave
2083/tcp  open     radsec
2086/tcp  open     gnunet
2087/tcp  open     eli
2095/tcp  open     nbx-ser
2096/tcp  open     nbx-dir
3306/tcp  open     mysql
7984/tcp  filtered unknown
8984/tcp  filtered unknown
9999/tcp  filtered abyss
10050/tcp open     zabbix-agent

Nmap done: 1 IP address (1 host up) scanned in 780.82 seconds
```
What is all this stuff? All this time I hadn't yet opened up these addresses in my browser because I was a little nervous about what I'd find, so I checked them with curl instead.

```
👻🌵✨$ curl номе.рф
<html><head><META HTTP-EQUIV="refresh" CONTENT="0;URL=/cgi-sys/defaultwebpage.cgi"></head><body></body></html>
👻🌵✨$ curl hosting18.ukrnames.com
<html><head><META HTTP-EQUIV="refresh" CONTENT="0;URL=/cgi-sys/defaultwebpage.cgi"></head><body></body></html>
👻🌵✨$ curl xn--e1ance.xn--p1ai
<script language="JavaScript">
  window.location.href = "https://nnxoe.topgirlshere.com/c/da57dc555e50572d?s1=22177&s2=96501&s3=new_1&j1=1&j3=1"
</script>%                                                                    
```
Aha!! So номе.рф and hosting18.ukrnames.com both go to the same default nginx server page (if you can't tell from those results those domains auto redirect to cpanel's default page saying that perhaps that page's IP address had changed). But xn--e1ance.xn--p1ai is just a page with a script that auto redirects you to something called "topgirlshere". Well I have a pretty good guess what lies down that road.

But what is the endgame of this text message scam? And why do they have so much else going on with their server? And how can an IP have so many domains attatched to it? See you tomorrow.
