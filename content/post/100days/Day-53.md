+++
title = "Shodan Stories Day 53: Just an IoT Highway Sign in Los Angeles"
date = 2019-02-25T19:46:10-05:00
draft = false
tags = []
categories = ["100 days"]
+++

I had a red eye flight last night and am deliriously sleepy, and somewhere in this state bubbled up a strong desire to find an electronic highway billboard and read what it said remotely. I read [Skyline](https://www.skylineproducts.com/) makes internet connected billboards and use port 161. So I got searching.

## A Skyline Sign on 173.4.137.205
Skyline manufactures quite a few different kinds of signs, but all of them are related to car transit.
![](/images/100Days/Day53/skyline.png)

I found a few dozen results, all of them in the US, and I picked one in Los Angeles, with the thought that as the center of American car culture LA might have some interesting signs.

On port 161 the IP was running a service that used the [Simple Network Management Protocol](https://en.wikipedia.org/wiki/Simple_Network_Management_Protocol). I installed a set of [SNMP Python tools](http://snmplabs.com/snmpclitools/snmpget.html) to try and see if I could make a request for the contents of the sign, but given my aforementioned sleep deprivation addled state I couldn't figure out how to make it work. I could definitely connect, but then had no idea what kind of flags to use etc and none of the examples I was seeing would work. Maybe it just was refusing me as I wasn't authenticated, who knows. It was also running telnet servers on 23 and 2332, but both of those require logins.
![](/images/100Days/Day53/acemanager.png)
On 9091 and 9443 it was running a login for a [Sierra Wireless](https://www.sierrawireless.com/) [Acemanager AirLink](https://www.sierrawireless.com/resources/QtrlyNewsletters/Announcements/AceWare_Mar08_Announce/AceWare_Mar08_announce.html) login. If you remember from back on day 32, the Sierra Wireless AirLink is a rugged router for remote outdoor locations.
![](/images/100Days/Day53/behind.png)
That makes sense given that it's a road sign of some kind. I was able to find the contentless xml of what's past the login screen. Even if I could log in, it doesn't look like there would be any clues about what the sign actually said.

I went back and futzed with the SNMP a bit more, but realized that it's not reaching out into the world and reading some random digital street sign that I needed. What I needed was a nap. See you tomorrow.
