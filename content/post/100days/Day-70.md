+++
title = "Shodan Stories Day 70: Engineering Consulting in Tangier, WampServer, and You'll Always Have a Job with PHP"
date = 2019-03-14T22:18:19-04:00
draft = false
tags = []
categories = ["100 days"]
+++


Today I truly cast a stone into the sea blindfolded, and decided to see what typing in just any old random IP address into Shodan would bring up.

## WampServer on 197.230.101.90
I'm not sure what force compelled me to type 197.230.101.90, but it was indeed in Shodan and looked like it was running a website (80 and 443 were serving HTTP) and SQL databases (3306, the [mySQL](https://www.mysql.com/) database port and 5432, the [PostgreSQL](https://www.postgresql.org/) port were both running). And it looked like a Windows machine, because 137 was running [NetBIOS](https://en.wikipedia.org/wiki/NetBIOS). Before checking the webserver though, I checked WhoIS and DNS, and while the IP address doesn't look like it's tied to a DNS address (i.e. has no url), the IP address is in a block of addresses fixed to "Tanger Med engineering".
```
inetnum:        197.230.101.88 - 197.230.101.95
netname:        Fixed_B2B
descr:          Fixed B2B Orange Maroc Customer Tanger Med engineering
country:        MA
admin-c:        EMB1-AFRINIC
admin-c:        RK36-AFRINIC
tech-c:         EMB1-AFRINIC
tech-c:         RK36-AFRINIC
status:         ASSIGNED PA
mnt-by:         meditel-MNT
source:         AFRINIC # Filtered
parent:         197.230.0.0 - 197.230.255.255
```
That confirmed for me what Shodan had already told me, that this IP was in Morocco, as Tanger Med is the name of a [huge port complex in Tangier](https://www.tangermed.ma/en/), and Orange Maroc is [the Moroccan subsidiary of Orange, the French telecom giant](https://en.wikipedia.org/wiki/Orange_S.A.).

According to their [LinkedIn page](https://www.linkedin.com/company/tme-tanger-med-engineering-/about/), Tanger Med Engineering is a subsidiary of the Tanger Med ownership company, and specializes in international consulting on large-scale infrastructure engineering. Now for something interesting. Tanger Med Engineering's website, which their LinkedIn indicates is www.tme.ma, does not work, giving a "refused to connect" error. And I think I know why. Let's get back to the original IP.
![](/images/100Days/Day70/firstlook.png)
The website it's running is a configuration page for a [WampServer](http://www.wampserver.com/en/). WampServer is "a Windows web development environment which allows you to create web applications with Apache2, PHP and a MySQL database". Most of those little links you see there are just full of PHP, and I'm reminded of a Vine video I saw years ago that was just a fake PHP ad that said "You'll always have a job with PHP". PHP has been going strong for almost 25 years, but Vine is gone forever. RIP Vine.

My own life is a little too short to spend too much time looking at PHP, so I focused on the two non-PHP links, TME and TMMS down at the bottom. Now I'm sure you've guessed it already, TME does indeed stand for Tanger Med Engineering, and yes indeed, this is their missing website.
![](/images/100Days/Day70/tme.png)
Why is it here? My guess is that they are working on it, and this WampServer is a Tanger Med staging ground for web development. I don't know why they wouldn't just host a placeholder or an older version of their website at their main URL, but what do I know.
![](/images/100Days/Day70/tmms.png)
TMMS stands for Tanger Med Marine Simulator, which is another subsidiary of Tanger Med. They do training for ship captains and pilots. It's specifically... a [room made to look like a boat helm](http://www.tmpa.ma/en/activites-services/tanger-med-marine-simulator/)?
