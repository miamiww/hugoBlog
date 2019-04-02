+++
title = "Shodan Stories Day 82: Monitoring Modbus Logic Controllers in Wroclaw"
date = 2019-03-31T20:28:55-04:00
draft = false
tags = []
categories = ["100 days"]
+++

Saw a search today for "Modbus Gateway". I wasn't sure what that would be exactly so I thought I'd take a look.

## Modbus Gateway on 82.143.179.14
[Modbus](https://en.wikipedia.org/wiki/Modbus) is a protocol for communication over serial developed in 1979, originally meant for logic controllers, but now with wide use across industrial electronic devices. A [modbus gateway](http://www.protocolindia.com/products/prd-gprs-gateways/modbus-gateway/) is a device for connecting modbus devices into IP networks (sometimes the internet), typically so that they can be remotely monitored. They mostly look like little boxes with serial ports and an ethernet port, but some of them have wifi in addition to or instead of ethernet.

This search (for 502 modbus) had about 200 results, most of which were in Poland, so I picked one in Poland. The search was picking up gateways based on the results from their FTP ports.
![](/images/100Days/Day82/modbus.jpg)
That image could be the very model of modbus I found. I couldn't figure much out about mine, however. It was running an FTP port, which required authorization for access, and nothing else. I would assume FTP is being used to access log files that the device is creating. Not very exciting, but interesting all the same. 

See you tomorrow.
