+++
title = "Day 5: Organic Chemistry in Poland, Ecotoxicology, and the Dangers of Static Electricity"
date = 2019-01-08T13:33:49-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I decided to go looking for [MySQL](https://en.wikipedia.org/wiki/MySQL) databases. I've always loved SQL, it was one of the first "programming languages" I learned and was a big part of one of my first jobs.


### Institute of Industrial Organic Chemistry on 79.96.39.102
Checking with [MySQL documents](https://dev.mysql.com/doc/mysql-port-reference/en/mysql-ports-reference-tables.html) I found that MySQL databases typically run off of port 3306. So I went on Shodan to look for things with port 3306. One of the first results I saw was from Poland, and being Polish I couldn't resist poking around a bit in the homeland.

I started off looking at it with `nmap`.
```
👻🌵✨$ nmap 79.96.39.102
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-08 13:51 EST
Nmap scan report for cloudserver060808.home.pl (79.96.39.102)
Host is up (0.12s latency).
Not shown: 915 filtered ports, 68 closed ports
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
25/tcp   open  smtp
80/tcp   open  http
110/tcp  open  pop3
143/tcp  open  imap
443/tcp  open  https
465/tcp  open  smtps
587/tcp  open  submission
990/tcp  open  ftps
993/tcp  open  imaps
995/tcp  open  pop3s
1433/tcp open  ms-sql-s
1443/tcp open  ies-lm
3306/tcp open  mysql
3690/tcp open  svn
5432/tcp open  postgresql
```
Lots of ports open, it looks like this IP has a bunch of functions, including email (25, 110, 143, 465, 587, 993, 995), a webpage (80 and 443), and databases (all those ports with sql). Just based on the ports this looks like a corporate server for sure. Going to the IP in a browser confirms this...
![](/images/100Days/Day5/IPO2.png)
The Institute of Industrial Organic Chemistry (IPO)! No I've never heard of it before but their website is a delight of early 00s web design. They were formed in 1947 and have 50-100 employees, and act as a industry research institute to the chemical industry, providing independent studies on the efficacy and toxicology of newly developed chemical compounds. I assume that regulation prevents chemical development companies from doing their own reports on the safety of their newly developed products, so they hire companies like IPO to do the testing for them. IPO has an entry on [Crunchbase](https://www.crunchbase.com/organization/institute-of-industrial-organic-chemistry#section-overview):


_The Institute of Industrial Organic Chemistry (IPO), Branch Pszczyna is a leading research and development centre with more than 65 years of tradition which performs a wide variety of toxicological and ecotoxicological studies. The IPO conducts studies for companies worldwide, cooperates with both domestic and foreign research units as well as actively participates in the international EU and OECD research projects. The aim of the studies mentioned above is to evaluate possible harmful effects of various chemical substances on human health, animals and the natural environment. During the last 65 years the Institute has developed and established its position as one of the best-known research centers at home and abroad._

According to [IPO's website](http://www.ipo.waw.pl/ENG//) in addition to the primary work they do with [toxicology](https://en.wikipedia.org/wiki/Toxicology) and [ecotoxicology](https://en.wikipedia.org/wiki/Ecotoxicology) they do research on explosives, solid rocket fuels, pyrotechnics, and chemical weapons, though they have a specialization in static electricity hazards! For their ecotoxicological they do tests with birds, fish, aquatic organisms that aren't fish, bees, non-bee arthropods, earthworms, soil microorganisms, and plants. My mom studied chemistry in Poland and I started wondering if maybe she would have worked at a place like this had she stayed in the country. They have two offices, one in Warsaw and [another in Pszczyna](http://www.ipo-pszczyna.pl/pl/index), not too far away from where my family lives.

I tried poking at all the ports, but didn't find anything out of the ordinary. Everything seems secure, although Shodan did tell me that their version of postgresql was out of date and had a variety of exploitable vulnerabilities. But I did notice that the DNS entry for this IP resolves to `cloudserver060808.home.pl`. That's not what their URL actually is for their website, it's [www.ipo.waw.pl](http://www.ipo.waw.pl/). A little interesting, their webhost is giving them a specific non-public url. Checking out [home.pl](https://www.united-internet.de/en/newsroom/press-releases/press-releases-detail/news/united-internet-acquires-polish-webhosting-market-leader-homepl-and-considers-ipo-in-applications-s.html) I found it pretty easy to figure out the kind of plan that IPO had bought for their cloud server.
![](/images/100Days/Day5/TheHost.png)
Even just iconographically it's easy to see this is the one: a cloud server with email, a website, and databases.


What's the history for the three ring cylinder representing a database anyway? See you tomorrow.
