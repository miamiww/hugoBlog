+++
title = "Shodan Stories Day 6: Air Conditioning and Air Traffic Control in Yokohoma"
date = 2019-01-09T18:19:08-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I decided to look for more industrial control systems, specifically [Mitsubishi Q-Series logic controllers](https://us.mitsubishielectric.com/fa/en/products/controllers/programmable-controllers-melsec/melsec_q-series).

### Yokohama Air Traffic Control Tower on 133.34.157.13
Reading about them on Shodan it looks like the Q-Series logic controllers tend to run off ports 5006 or 5007. So I did a search for those open ports. Judging from the results it looks like the majority of these Mitsubishi controllers are in Japan, not surprising I suppose since Mitsubishi is a Japanese company. So I picked one of the first results. I've been finding that `nmap` is a pretty good first go-to tool since, `host`, `whois`, and `nslookup` depend on DNS records, and quite a few things aren't on DNS.

```
👻🌵✨$ nmap -p- 133.34.157.13
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-09 20:32 EST
Nmap scan report for 133.34.157.13
Host is up (0.23s latency).
Not shown: 65529 filtered ports
PORT      STATE  SERVICE
21/tcp    open   ftp
23/tcp    closed telnet
80/tcp    open   http
502/tcp   open   mbap
5007/tcp  open   wsm-server-ssl
30301/tcp open   unknown

Nmap done: 1 IP address (1 host up) scanned in 1431.86 seconds
```
One interestingly bit, port 502 is running mbap which is the [Modbus](https://en.wikipedia.org/wiki/Modbus) protocol for [serial communication](https://en.wikipedia.org/wiki/Serial_communication).

Very interestingly though port 80 is open even though I couldn't find anything about this IP on `nslookup`, meaning it's running something via http for a browser to interpret but doesn't have a URL. So taking a look via a browser...
![](/images/100Days/Day6/DL8.png)
I was pretty dumbfounded by what I was looking at. Yokohama Air Control Tower... as in Air Traffic Control? After looking around quite a bit, near as I can tell this is indeed a data logger for the facility management system for an air traffic control tower in Yokohama. I couldn't really find much about an airport in Yokohama, it seems that there isn't a major airport but there is a small airfield for private or government flights. It has an airport code, [YOK](https://www.world-airport-codes.com/japan/yokohama-7799.html), but you can't book a flight there, and travel guides all recommend flying into Tokyo's Haneda airport. There's also heliports... English language sources are scarce and I'm not sure what to search for in Japanese to find out more.
![](/images/100Days/Day6/data.png)
But I can find out about the amount of power demand from this building's lighting and air conditioning. I'm guessing that the other measurements have to do with water.
![](/images/100Days/Day6/data2.png)
It seems like I could actually make changes to things here but I resisted the urge to hit too many buttons. But I did find that they had conveniently left the telnet login on this web app.
![](/images/100Days/Day6/Telnet.png)
Whoops! Possibly that's why port 23 is closed.

Looking at the other obvious info on this web app, [MSYSTEM](http://www.m-system.com/english/index.html) is a manufacturer of a variety of data loggers and logic controllers, and the DL8 is their series of web-based data loggers.
![](/images/100Days/Day6/MSeries.png)
So this wasn't what I had originally gone searching for, a Mitsubishi Q-Series. They must be using 5007 for something else.
![](/images/100Days/Day6/MSeries2.png)
Sure looks familiar so this is definitely what is behind this IP.

But why collect water quality levels in a seemingly nonexistent air traffic control tower? Who's really running this operation. See you tomorrow.
