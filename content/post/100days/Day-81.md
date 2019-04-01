+++
title = "Shodan Stories Day 81: Microwave Access in Ghaziabad"
date = 2019-03-31T12:54:32-04:00
draft = false
tags = []
categories = ["100 days"]
+++

Today a search for "unprotected WiMAX towers". The word tower was pretty tantalizing. The actual search was for "OX253P".

## WiMAX Tower on 117.244.48.33
[WiMAX](https://en.wikipedia.org/wiki/WiMAX) is a communication standard meant to give [last mile](https://en.wikipedia.org/wiki/Last_mile) wireless access to the internet to homes and businesses using microwaves. This would be a wireless alternative to DSL and cable internet, not requiring any cabling to the home endpoint, only a receiver antenna, much like LTE. It works much in the same way as cell towers, and frequently [WiMAX and cell towers are bundled into one](https://gizmodo.com/giz-explains-how-cell-towers-work-5177322). It's not used much in North America, because there was so much existing copper infrastructure, but it's popular in many other countries. All the results in my search were from India, so I picked one at random.

It was running [SNMP](https://en.wikipedia.org/wiki/Simple_Network_Management_Protocol) on port 161 and a webserver on 80.
![](/images/100Days/Day81/firstlook.png)
I believe this is actually someone's home antenna, and not a tower. Judging from the [user manual](https://fccid.io/I88OX253P/User-Manual/User-Manual-1403055) the default password is admin/admin. But of course I didn't try it :)

See you tomorrow.
