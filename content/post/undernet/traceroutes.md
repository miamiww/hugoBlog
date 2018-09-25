+++
title = "Traced Routes"
date = 2018-09-17T22:07:07-04:00
draft = false
tags = []
categories = ["understanding networks"]
+++

The websites I visit most frequently are a little boring. According to what Chrome, my browser, suggests, my number one visited website is __Twitter__, followed by the (in?)famous data journalism blog __[FiveThirtyEight](fivethirtyeight.com)__, then __ScaryGoRound.com__ which is a webcomic I've been reading for almost 15 years, then __Gmail__ (the [Inbox](inbox.gmail.com) flavor), then __Github__, and then __my own blog__ which you are reading now. I think that last one is only because of how often I need to double check that my posts have actually made it online, not because of the love I have for my own posts. For the most part I use the internet from my home network and NYU's network. I also make use of my cell network but I don't know how to check those data.

So I divided up my investigation into six websites from two locations. I used `traceroute`, `whois`, my browser, a [GeoIP Lookup Tool](https://www.ultratools.com/tools/geoIpResult), `nslookup`, `host`, and `nmap` just in case someone left a port open :)


Two examples of routes:

* From my apartment to Twitter:
```
1  192.168.0.1 (192.168.0.1)  5.638 ms  0.887 ms  0.881 ms
2  * * *
3  be61.nycynymy01h.nyc.rr.com (68.173.202.72)  27.807 ms  13.267 ms  14.582 ms
4  agg113.nyclnyrg01r.nyc.rr.com (68.173.198.40)  39.157 ms  17.721 ms  19.290 ms
5  bu-ether29.nwrknjmd67w-bcr00.tbone.rr.com (107.14.19.24)  37.255 ms  22.960 ms
   bu-ether19.nwrknjmd67w-bcr00.tbone.rr.com (66.109.6.78)  20.827 ms
6  66.109.5.138 (66.109.5.138)  20.463 ms  17.167 ms
   bu-ether12.nycmny837aw-bcr00.tbone.rr.com (66.109.6.27)  28.781 ms
7  0.ae4.pr0.nyc20.tbone.rr.com (66.109.1.35)  14.340 ms  26.917 ms  19.967 ms
8  r-199-59-151-90.twttr.com (199.59.151.90)  18.630 ms  15.155 ms  14.880 ms
9  * * *
10  104.244.42.1 (104.244.42.1)  43.585 ms  39.181 ms  35.576 ms
```


* From NYU to Twitter:
```
1  10.17.0.2 (10.17.0.2)  1.657 ms  1.396 ms  1.274 ms
2  nyugwa-new-vl901.net.nyu.edu (128.122.1.4)  1.527 ms  2.302 ms  5.124 ms
3  192.168.184.228 (192.168.184.228)  2.603 ms  4.234 ms  2.962 ms
4  nyugwa-outside-ngfw-vl3080.net.nyu.edu (128.122.254.114)  2.589 ms  2.445 ms  2.276 ms
5  192.168.184.221 (192.168.184.221)  2.365 ms  6.247 ms  4.148 ms
6  nyugwa-vl1001.net.nyu.edu (192.76.177.202)  5.306 ms  2.640 ms  2.500 ms
7  dmzgwb-ptp-nyugwa-vl3082.net.nyu.edu (128.122.254.111)  2.748 ms  2.977 ms  3.093 ms
8  extgwc-ptp-dmzgwb.net.nyu.edu (128.122.254.74)  2.782 ms  2.841 ms  2.663 ms
9  6-1-30.ear3.newyork1.level3.net (4.28.130.117)  3.075 ms  3.406 ms  3.168 ms
10  twitter-inc.ear3.newyork1.level3.net (4.15.212.254)  3.281 ms  2.869 ms  6.757 ms
11  * * *
12  104.244.42.1 (104.244.42.1)  28.849 ms  22.204 ms  20.625 ms
```

### The At Home Analysis
All my routes from home had the same exact five first lines, with the first being my router. Poking around the next four (well three really since 2 is always a mystery bounce) I found that, unsurprisingly they all belong to Time Warner, my ISP, and they all had _nearly_ identical WhoIs entries.

```
OrgName:        Time Warner Cable Internet LLC
OrgId:          RRNY
Address:        6399 S Fiddlers Green Circle
City:           Greenwood Village
StateProv:      CO
PostalCode:     80111
Country:        US
RegDate:        2000-09-27
Updated:        2018-03-07
Comment:        Allocations for this OrgID serve Road Runner residential customers out of the New York City, NY and Syracuse, NY RDCs.
Ref:            https://rdap.arin.net/registry/entity/RRNY


OrgAbuseHandle: ABUSE10-ARIN
OrgAbuseName:   Abuse
OrgAbusePhone:  +1-703-345-3416
OrgAbuseEmail:  abuse@rr.com
OrgAbuseRef:    https://rdap.arin.net/registry/entity/ABUSE10-ARIN

OrgTechHandle: IPADD1-ARIN
OrgTechName:   IPAddressing
OrgTechPhone:  +1-314-288-3111
OrgTechEmail:  ipaddressing@chartercom.com
OrgTechRef:    https://rdap.arin.net/registry/entity/IPADD1-ARIN
```

Time Warner I know about because they send me a bill each month, but what is Road Runner New York (RRNY)? Apparently it is Time Warner's attempt to brand their high speed internet service as a commodity, [dating back to 1998](https://www.warnermediagroup.com/newsroom/press-releases/1998/03/20/time-warner-unveils-road-runner-high-speed-online-service-for). And apparently I must have [Road Runner® Turbo with PowerBoost®](https://www.timewarnercable.com/en/about-us/press/time_warner_cableroadrunnerbroadbandandturbocustomersreceivespee.html), but it's a shame that even as a reliable customer I'm no longer able to access [the fastest Road Runner® customer portal ever](https://www.timewarnercable.com/en/about-us/press/time_warner_cablelaunchesthefastestroadrunnercomever.html).
Now I said nearly identical WhoIs entries, the only difference between them being that the last IP address carried a slightly differing comment:
```
Comment:        Allocations for this OrgID serve Road Runner residential customers out of the Columbus, OH, Herndon, VA and Raleigh, NC RDCs.
```
So it seems that, oddly enough, either Time Warner has started to misallocate their region-defined IP addresses or my traffic was heading down South. Further investigation, as you will see, shows that the first is true.

However before getting into the IPs further down the line I thought that maybe those [ARIN](https://www.arin.net/) links would be interesting but they were all just JSON files and who has time to parse JSON in 2018. Well apparently I do or I love procrastinatory yak-shaving because I looked through them.

Some interesting bits:
* Time Warner has something of a formalized process for law enforcement tracking IP ownership, but it's linked to under the Charter/Spectrum brand part of their web presence, a cautionary tale to the dangerous obfuscatory pitfalls of corporate mergers:
```
{
"title": "Registration Comments",
"description": [
"IP Addressing is used for corporate IP allocation and administration, we are unable to provide or reply to inquires regarding specific IP address lookups or subscriber information. ",
"",
"Law Enforcement Officials please visit:  http://www.charter.com/lea  for assistance on subpoena, identification, and escalations. This information is for Law Enforcement officials only."
]
}
```

* Road Runner owns big blocks of IPs, which are "NON-PORTABLE", which probably has a specific meaning.
```
"handle": "NET-24-194-0-0-1",
"startAddress": "24.194.0.0",
"endAddress": "24.195.255.255",
"ipVersion": "v4",
"name": "ROADRUNNER-NYS-4BLK",
"parentHandle": "NET-24-0-0-0-0",
"remarks": [
{
"title": "Registration Comments",
"description": [
"ADDRESSES WITHIN THIS BLOCK ARE NON-PORTABLE"
]
}
]
```

* Road Runner's Registration IP is the deeply sinister `66.66.0.0`, which I can only assume given the packet loss in trying to ping it is buried in the depths of hell.

```
👻 🌵 ✨ $ ping -c 3 66.66.0.0
PING 66.66.0.0 (66.66.0.0): 56 data bytes
Request timeout for icmp_seq 0
Request timeout for icmp_seq 1

--- 66.66.0.0 ping statistics ---
3 packets transmitted, 0 packets received, 100.0% packet loss
```


Back to the New York or Virginia issue, the subsequent IP always seemed to be close enough to New York it didn't seem like it was going down to Virginia/NC right away. How they all shake out:

* My blog website's trace record goes dark at this point, giving only empty bounces after the final Road Runner trace

* FiveThirtyEight switches to Comcast's servers in Newark before going dark

* Github goes to [Level3](http://www.level3.com/en/) in Newark and then to Level3 in Washington DC and then goes dark

* ScaryGoRound ends up at the seemingly hegemonic [Tata Communications's routers](https://www.tatacommunications.com/) in Newark for seven or so hops before ending up well... here
```
13  cyclone.yadda.net (50.116.60.26)  3.889 ms  4.771 ms  4.089 ms
```
at [Linode's](www.linode.com) servers on 329 E. Jimmie Leeds Road Suite A, Galloway NJ. To get that address I used the delightful [Data Center Map](https://www.datacentermap.com/). But what is cyclone.yadda.net? It exists as a web page but the content there defies both my capacity and my will to understand. Maybe Don Sutherland owns Linode?

* Gmail makes one hop to Tata here in NYC but then hops onto Google's IPs for three hops and never leaving NYC, I assume going to either their office here or some data center they were able to buy on the High Line or something, I don't know what they are capable of doing. Thus far we've only made it to Washington D.C. but...

* Twitter seems to go all the way to the top. Which is to say, to California. After two subsequent hops in the Time Warner family of routers it made a hop to Twitter's server in Raleigh Virginia and a * * * it looks like it goes directly to the bay area. I'm a little suspicious of the geoIP tools but I couldn't turn over anything to disagree with that. The Twitter WhoIs page was also a little interesting.


Instead of the perfunctory "IP abuse" faceless corporate email addresses (I'm looking at you network-abuse@google.com), Twitter includes the emails _and_ phone numbers of two real live human beings.
```
OrgTechHandle: YURCH-ARIN
OrgTechName:   Yurchenko, Anton
OrgTechPhone:  +1-408-207-2488
OrgTechEmail:  ayurchenko@twitter.com
OrgTechRef:    https://rdap.arin.net/registry/entity/YURCH-ARIN

OrgTechHandle: SOUTH69-ARIN
OrgTechName:   Southern, Timothy
OrgTechPhone:  +1-415-222-9670
OrgTechEmail:  tsouthern@twitter.com
OrgTechRef:    https://rdap.arin.net/registry/entity/SOUTH69-ARIN

OrgAbuseHandle: TNA33-ARIN
OrgAbuseName:   Twitter Network Abuse
OrgAbusePhone:  +1-415-222-9670
OrgAbuseEmail:  net-abuse@twitter.com
OrgAbuseRef:    https://rdap.arin.net/registry/entity/TNA33-ARIN

OrgTechHandle: NETWO3685-ARIN
OrgTechName:   Network Operations
OrgTechPhone:  +1-415-222-9670
OrgTechEmail:  noc@twitter.com
OrgTechRef:    https://rdap.arin.net/registry/entity/NETWO3685-ARIN
```

I became curious about these two Twitter employees, and I wanted to know why they had been added to the WhoIs record instead of leaving it with just the corporate accounts. What would happen if they quit? Would Twitter have to immediately update its record? Obviously the reasonable thing to do would be to call them but I chose instead to search for them online, but I began to feel a little weird and stopped once I found their LinkedIn profiles, birthdays, zip codes, and dating profiles.

### The At School Analysis

The biggest difference between at home and at school is the NYU network, which for the most part would make similar handoffs to Level3 or Comcast that Time Warner was making. All that I found particularly interesting about NYU's routers was that it received its IPs via 'Direct Assignment', and that it had been registered all the way back in 1984!

```
NetRange:       128.122.0.0 - 128.122.255.255
CIDR:           128.122.0.0/16
NetName:        NYU-NET
NetHandle:      NET-128-122-0-0-1
Parent:         NET128 (NET-128-0-0-0-0)
NetType:        Direct Assignment
OriginAS:
Organization:   New York University (NYU)
RegDate:        1986-05-01
Updated:        2017-11-27
Comment:        Please query Merit's RADb for up to date information on allocations, routing policy, and contacts.
Comment:
Comment:        whois -h whois.radb.net
Comment:
Comment:        www.ra.net
Ref:            https://rdap.arin.net/registry/ip/128.122.0.0


OrgName:        New York University
OrgId:          NYU
Address:        726 Broadway, 8th Floor - ITS
City:           New York
StateProv:      NY
PostalCode:     10003
Country:        US
RegDate:        1984-07-04
Updated:        2017-11-27
Ref:            https://rdap.arin.net/registry/entity/NYU


OrgNOCHandle: COSI-ARIN
OrgNOCName:   Communications Operations Services - ITS
OrgNOCPhone:  +1-212-998-3444
OrgNOCEmail:  noc-cosi-arin@nyu.edu
OrgNOCRef:    https://rdap.arin.net/registry/entity/COSI-ARIN

OrgAbuseHandle: OIS9-ARIN
OrgAbuseName:   Office of Information Security
OrgAbusePhone:  +1-212-998-3333
OrgAbuseEmail:  abuse@nyu.edu
OrgAbuseRef:    https://rdap.arin.net/registry/entity/OIS9-ARIN
```

There was only one other point of difference, one that I have no explanation for. In going to FiveThirtyEight from the NYU network, instead of heading to Comcast and bouncing around forever, it goes to 60 Hudson, then leaves the domain of ARIN and hops [RIPE](https://www.ripe.net/), first to [Tiscali International's](https://en.wikipedia.org/wiki/Tiscali) German servers and then to TeliaNet in Sweden. Why a blog written in New York is sending me to Sweden is A MYSTERY.





__End Note__: I did try to `nmap` things but never found any open ports. Guess the net's wild wild west days are over. Maybe it's time for this old console cowboy to hang up his hat.
```
Starting Nmap 7.70 ( https://nmap.org ) at 2018-09-17 00:24 EDT
Nmap scan report for be61.nycynymy02h.nyc.rr.com (68.173.202.74)
Host is up (0.018s latency).
All 1000 scanned ports on be61.nycynymy02h.nyc.rr.com (68.173.202.74) are closed

Nmap done: 1 IP address (1 host up) scanned in 40.26 seconds

```
