+++
title = "Shodan Stories Day 15: Deftly Avoiding Turning On A Stranger's Lights in Bologna, the Commercial Level ESP2866, Getting Too Close with WiGLE, and What's the Deal with Home Automation Anyway?"
date = 2019-01-18T11:01:04-08:00
draft = false
tags = []
categories = ["100 days"]
+++

Another IoT home device today. At this point I'm picturing the people with these things basically having a [Wallace and Gromit style](https://www.youtube.com/watch?v=pqGTtFIZm5Y&t=65) lifestyle (note: I do have a wifi plug and yes this is my lifestyle). This one was inspired by another search I didn't recognize, for "Sonoff".

## A Sonoff wifi enabled plug on 87.20.184.148
[Sonoff is a company](https://sonoff.itead.cc/en/) that makes IoT plugs and switches, as well as a couple of models of IoT fans and light bulbs. What's interesting about Sonoff is that many of their cheapest switches are just [ESP8266 boards](https://en.wikipedia.org/wiki/ESP8266) with a casing, [making them very](https://tzapu.com/sonoff-firmware-boilerplate-tutorial/) [easy to hack](https://medium.com/@jeffreyroshan/flashing-a-custom-firmware-to-sonoff-wifi-switch-with-arduino-ide-402e5a2f77b).
![](https://github.com/arendst/arendst.github.io/blob/master/media/sonoffbasic.jpg)
I just picked the first Sonoff that showed up in my Shodan search, in Italy. Shodan said it was running a web app on port 80, so I checked it out in a browser.
![](/images/100Days/Day15/mainmenu.png)
The firmware's out of date! Probably should get that taken care of. More interestingly there is a big old Toggle button calling out to be toggled. If it's a switch that probably turns the current on and off so I resisted.

Looking up Sonoff-Tasmota I found that it is a [homebrewed version of the Sonoff firmware](https://github.com/arendst/Sonoff-Tasmota), so this device is either a hacked Sonoff original or a [Sonoff clone running off of someone's ESP8266 board](https://community.blynk.cc/t/sonoff-clone-mini-esp8266-power-ac-relay-controller/9549/4). Let's check out that console!
![](/images/100Days/Day15/console.png)
Looks like it's mostly been taking commands via [MQTT](http://mqtt.org/). Looking more closely... there's the wifi name! "Angelozzi". Well what could we do with that information? Check it on [WiGLE](https://wigle.net/index) of course!
![](/images/100Days/Day15/wigle.png)
WiGLE is a global database of wifi and cell networks, promising "All the networks. Found by Everyone." They tag SSID names and other information to latitude and longitudes. And yes it looks like they had six wifi networks named "Angelozzi", three of which were in New Jersey, one in Canada, one in South Africa, and yes, one in Italy. In Bologna. Again I get the vertigo of overconnection.

I decided to give it an `nmap` just for good measure.
```
👻🌵🔮 $ nmap -p-  87.20.184.148
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-18 12:33 PST
Nmap scan report for host148-184-dynamic.20-87-r.retail.telecomitalia.it (87.20.184.148)
Host is up (0.26s latency).
Not shown: 65530 filtered ports
PORT     STATE  SERVICE
80/tcp   open   http
3218/tcp open   smartpackets
5001/tcp closed commplex-link
7170/tcp open   nsrp
8123/tcp open   polipo

Nmap done: 1 IP address (1 host up) scanned in 899.80 seconds
```
As soon as I did though I noticed that something weird was happening on the console: the Sonoff had lost connection with whatever device had been MQTTing it?
![](/images/100Days/Day15/whoops.png)
What this because I'd started flooding it with ping probes? Possibly? It seemed to be able to connect again once my scan was done. After a little fiddling around with these ports I found that the Sonoff device was talking with an [open source home automation system called Home Assistant](https://www.home-assistant.io/), which must be the device it's MQTTing to at 192.168.1.100, using [the classic MQTT port of 1883](https://mqtt.org/faq).
![](/images/100Days/Day15/homeassistant.png)
[It's probably running on a Raspberry Pi](https://www.home-assistant.io/getting-started/). See you tomorrow.


PS here's my tavel traceroute, from Bru Coffee in LA to Bologna, Italy.
```
👻🌵🔮 $ traceroute 87.20.184.148
traceroute to 87.20.184.148 (87.20.184.148), 64 hops max, 52 byte packets
 1  192.168.0.1 (192.168.0.1)  13.126 ms  4.592 ms  5.124 ms
 2  142.254.237.217 (142.254.237.217)  41.680 ms  29.273 ms  21.619 ms
 3  agg60.lsdwcaro02h.socal.rr.com (24.30.174.221)  24.239 ms  27.124 ms  17.349 ms
 4  agg21.lamrcadq02r.socal.rr.com (72.129.10.194)  32.097 ms  29.944 ms  28.588 ms
 5  agg28.tustcaft01r.socal.rr.com (72.129.9.2)  22.269 ms  31.283 ms  26.081 ms
 6  bu-ether16.tustca4200w-bcr00.tbone.rr.com (66.109.6.64)  23.669 ms  31.205 ms  25.566 ms
 7  bu-ether14.lsancarc0yw-bcr00.tbone.rr.com (66.109.6.4)  31.582 ms
    be4.clmkohpe01r.midwest.rr.com (107.14.19.37)  34.261 ms  34.340 ms
 8  ae2.lsancarc0yw-bpr01.tbone.rr.com (66.109.1.41)  29.547 ms
    0.ae0.pr1.lax00.tbone.rr.com (107.14.17.248)  19.141 ms  27.934 ms
 9  ix-ae-24-0.tcore1.lvw-los-angeles.as6453.net (66.110.59.81)  26.435 ms  40.361 ms  22.727 ms
10  if-ae-34-2.tcore2.dt8-dallas.as6453.net (66.110.57.20)  57.961 ms  57.910 ms  60.878 ms
11  if-ae-2-2.tcore1.dt8-dallas.as6453.net (66.110.56.5)  62.587 ms  56.098 ms  52.617 ms
12  64.86.92.131 (64.86.92.131)  62.522 ms  190.974 ms  160.970 ms
13  etrunk0.milano1.mil.seabone.net (195.22.209.215)  253.123 ms  196.899 ms  200.779 ms
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  * * *
29  * * *
30  * * *
31  * * *
32  * * *
33  * * *
34  * * *
35  * * *
36  * * *
37  * * *
38  * * *
39  * * *
40  * * *
41  * * *
42  * * *
43  * * *
44  * * *
45  * * *
46  * * *
47  * * *
48  * * *
49  * * *
50  * * *
51  * * *
52  * * *
53  * * *
54  * * *
55  * * *
56  * * *
57  * * *
58  * * *
59  * * *
60  * * *
61  * * *
62  * * *
63  * * *
64  * * *
```
