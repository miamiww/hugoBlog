+++
title = "Shodan Stories Day 24: Watching the News in Cheongju, IPTime Routers, Synology Yet Again, and TVheadend"
date = 2019-01-27T17:16:00-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I saw a search just for "TVheadend" and I thought it looked like a weird name so I decided to investigate.

## TVheadened Server on 125.181.166.200

[TVheadend](https://tvheadend.org/) is an open source streaming server and recorder for streaming television on Linux, FreeBSD, or Android machines. I believe it works by intercepting television input and putting it into streamable format, which means that the machine running this server would need some kind of cable or radio tv receiver (maybe even a Dreambox 😄). It seemed like 50% of all the TVheadend servers were running in Korea, so I decided to pick a Korean one. Most of them had passwords to prevent viewing the server port but I managed to find one that did not.
![](/images/100Days/Day24/tvheadend.png)
It looked a little bit like the TV Guide channel I remember watching when I was home from school sick growing up. I remember just staring at the channel names scrolling by, an infinite expanse of boredom ahead of me. I tried to use Google translate here but it didn't do too good of a job. There were options for configuring at the top and those little orange bars in the column to the left are some kind of progress bar, but most of the rest remained untranslated. There were little icons at the left of each row that looked like TVs with a play button and I found that yes, clicking on one did indeed start playing TV.
![](/images/100Days/Day24/morningnews1.png)
After looking around I realized that each row is a distinct "stream", but in this case the server owner had only chosen to stream three stations,
[SBS](https://en.wikipedia.org/wiki/Seoul_Broadcasting_System),
[KBS1](https://en.wikipedia.org/wiki/KBS1), and
[MBS](https://en.wikipedia.org/wiki/Munhwa_Broadcasting_Corporation)
and that each row was a different streaming source of one of those networks. After watching all three for a little bit I found that they were all playing the morning news and all on relatively similar topics.
![](/images/100Days/Day24/morningnews2.png)
Those topics were boy bands, the weather, [Xi Jingping's possible meeting with Kim Jong Un](https://www.scmp.com/news/china/diplomacy/article/2181455/xi-jinping-accepts-offer-visit-pyongyang-says-north-korea-state), and [Japanese patrol planes getting too close to South Korean warships](https://www.japantimes.co.jp/news/2019/01/27/national/south-korea-defense-chief-lambastes-japan-alleged-flybys-near-naval-ships-orders-stern-action/).
![](/images/100Days/Day24/morningnews3.png)
I wanted to figure out what kind of device was running this, so I took a look at the other ports Shodan had indicated were open, 443 and 5001. HTTPs was running what looks awfully like a [Synology Web Station default page](http://blog.e-nnov.fr/en/synology-dsm-en/webstation/). It looks like Synology products have become very popular as a means to host ones one website or web services, because this is maybe the third time I've run into them.
![](/images/100Days/Day24/synologyA.png)
Port 5001 confirmed it, as it looks exactly like the logins for [Synology Network Attached Storage](https://www.synology.com/en-us/solution/what_is_nas) devices I'd seen in the past.
![](/images/100Days/Day24/synologyB.png)

Interesting, so it appears that this TV stream is running off of a Synology NAS. I noticed one other interesting thing though, which is that the SSL certificate for 443 was registred to "cheolsoon.com". Checking that host I found that I had been on cheolsoon.com all along!
```
➜  sandbox git:(master) ✗ host cheolsoon.com
cheolsoon.com is an alias for cholsoon.iptime.org.
cholsoon.iptime.org has address 125.181.166.200
```

What's that iptime.org thing you ask? Well [IPtime is a popular manufacturer of routers in Korea](http://iptime.com/iptime/), and apparently they allow you to easily [set up a CNAME via their URL to set up a URL for your own router](http://blog.kr.dnsever.com/?p=349), hence the cholsoon.iptime.org. From there it's pretty easy to give that URL an alias, in this case cheolsoon.com. So this TV streamer then is running a Synology Desk Station in their home in order to stream TV and possibly host a website in the future, and their home router is an IPtime model.
![](/images/100Days/Day24/IPtime.png)

Sounds like a pretty sweet setup! See you tomorrow.
