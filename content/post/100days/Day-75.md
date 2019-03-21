+++
title = "Shodan Stories Day 75: Powerful Routing in Karachi"
date = 2019-03-20T20:22:27-04:00
draft = false
tags = []
categories = ["100 days"]
+++

Today's the kind of day where I just don't remember how I found the IP I decided to write about. The dangers of looking in the morning and writing at night.

## VoIP WiMAX Gateway on 115.167.115.93
Today's just a router. Well not "just" I router I suppose, it's a powerful router.
![](/images/100Days/Day75/firstlook.png)
The configuration page was running on port 8080, but fortunately for them they had a password and it wasn't a default.

The router is a Gigaset SX686, which as far as I can tell is a "high performance" router for VoIP. It was manufactured by [Sagemcom](https://www.sagemcom.com/), a French telecom.
![](/images/100Days/Day75/gigaset.png)
Sagemcom has a typical business model for a telecom these days, heavily advertising its smart city and iot branches alongside their core comptetency of manufacturing residential networking equipment.
![](/images/100Days/Day75/diverse.png)
I figured out that this router was probably supplied to the user by the ISP, [Qubee](http://qubee.com.pk/join-in/), since Qubee advertises that they supply Sagemcom equipment.

They also advertise using the term "big data" in a wave I've never seen before.
![](/images/100Days/Day75/youtube.png)
Qubee is the Pakistani brand name for the broadband of a Dutch multinational company named [Augere](https://en.wikipedia.org/wiki/Augere). They also serve broadband in Bangladesh, and apparently had plans to expand to Uganda and Rwanda in 2011 according to some old press releases but as of today I couldn't find any sign that they succeeded in that expansion.

See you tomorrow.
