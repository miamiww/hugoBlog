+++
title = "Shodan Stories Day 54: Pumping Your Own in Saint-Denis"
date = 2019-02-26T19:43:36-05:00
draft = false
tags = []
categories = ["100 days"]
+++

I read this [old blog post from 2015](https://www.ericzhang.me/gas-station-atgs-exposed-to-public/) talking about how many internet connected pumps at gas stations were vulnerable to hacking. I wanted to see if anything had really changed in the last four years.

## Automated Tank Gauge on 81.248.205.246
Based on that blog post it seemed that the best thing to search for was "I20100". I immediately found several thousand results and yes all of them seemed to be accessible. I picked one in Réunion thinking that it would probably be the only time I would find something from there given its tiny population. Following what the blog post indicated I should do, I used `netcat` to connect to one of the ports and print out a status report from the gauges.

```
➜  ~ nc -v 81.248.205.246 10001
found 0 associations
found 1 connections:
     1:	flags=82<CONNECTED,PREFERRED>
	outif ipsec0
	src 10.6.6.182 port 61602
	dst 81.248.205.246 port 10001
	rank info not available
	TCP aux info available

Connection to 81.248.205.246 port 10001 [tcp/scp-config] succeeded!
^AI20100

I20100
    27-02-19  7:23

845645 TOTAL CAMELIA
BVD DORET ST DENIS  



INVENT INTERNE          

CUVE PRODUIT             VOLUME TC VOLUME   CREUX     HAUT      EAU      TEMP
  1  SP R2.1 25M3          9576         0    14528   1015.4      0.0    30.69
  2  GO R3.1 30M3         23361         0     5609   1790.2      0.0    32.54
```

Aha, so I have what seems like an address: _845645 TOTAL CAMELIA
BVD DORET ST DENIS_.

In addition I get a report on the amount of oil in each of two tanks. Reading [an English language manual](https://www.ericzhang.me/wp-content/uploads/2015/01/576013-635.pdf) I learn that cuve is the tank number, produit (product in english) is the name of the tank, volume is the amount of oil in the tank at the current temperature, tc volume is what the volume would be at 60F degrees, creux (ullage in English) is the amount of space in the tank not taken up by oil, haut is the oil height, eau is the amount of water in the tank, and temp is just the current temperature. It seems as though the TC Volume measure is not working, but they have no water in them (which I think is good), and still have plenty of oil in them, although tank 1 is over half empty.
![](/images/100Days/Day54/address.png)
That is indeed an address, though the number is a bit of a red herring, as I now believe it is the internal numbering system for gas pump company in Rénion and other places called [Total](https://en.wikipedia.org/wiki/Total_Gas_%26_Power). As near as I can tell the station is on Blvd. Doret in Saint-Denis, though I still have not been able to figure out what Camelia means..
![](/images/100Days/Day54/station.png)
And here it is! The Google maps car didn't go down this street, but Total itself had uploaded an image of this location.

Looks like they have an actual deli counter with sandwiches. When was the last time you got sandwiches at a gas station? See you tomorrow.
