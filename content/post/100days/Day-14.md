+++
title = "Shodan Stories Day 14"
date = 2019-01-17T07:04:32-08:00
draft = false
tags = []
categories = ["100 days"]
+++

This is another find inspired by recent searches on Shodan. I saw searches "FHEM Home Automation" and I needed to know more.

## Fhem Home Automation Server on 85.190.248.171
Every single result for FHEM was from Germany. So I picked the first one and got going. Looking up [FHEM](https://www.fhem.de/) first on Google I found that it is an open source server software for doing home automation, built in perl and meant to be run on any kind of full time 24/7 computer, like a Raspberry Pi. It was made in Germany but has full English documentation.
![](/images/100Days/Day14/fhem.png)
Since I read that the servers were telnet enabled I first tried connecting to this IP via telnet on port 23. It was closed, so then I did a port scan via `nmap`, and wound up getting some errors that I still don't fully understand.

```
➜  nmap 85.190.248.171
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-17 14:35 PST
RTTVAR has grown to over 2.3 seconds, decreasing to 2.0
RTTVAR has grown to over 2.3 seconds, decreasing to 2.0
RTTVAR has grown to over 2.3 seconds, decreasing to 2.0
RTTVAR has grown to over 2.3 seconds, decreasing to 2.0
RTTVAR has grown to over 2.3 seconds, decreasing to 2.0
RTTVAR has grown to over 2.3 seconds, decreasing to 2.0
RTTVAR has grown to over 2.3 seconds, decreasing to 2.0
Nmap scan report for 85.190.248.171
Host is up (0.22s latency).
Not shown: 997 closed ports
PORT     STATE    SERVICE
9/tcp    filtered discard
5060/tcp open     sip
8083/tcp open     us-srv

Nmap done: 1 IP address (1 host up) scanned in 1771.98 seconds
```  
I didn't get anywhere with 9 or 5060 but 8083 is hosting a web page and I could see it in the browser.
![](/images/100Days/Day14/thehome.png)
Uh oh! No password on the telnet port? But what's the telnet port, since the usual one wasn't open? I went checking in the event logs to see if there were any clues.
![](/images/100Days/Day14/telnetport.png)
Aha! So it's 7072. However when I tried to log in I got an immediate rejection, like the port had been configured to only accept connections from a specific IP. Maybe whatever machine this server is running on has a firewall that the server software isn't acknowledging. There is quite a bit of information in the web page though, and I quickly got a bit uncomfortable with how much access I seemed to have.
![](/images/100Days/Day14/temperature.png)
![](/images/100Days/Day14/current.png)
I seemed to be able to access house data like temperature, power load, fan speeds, and more. And not just for the current day, but for every day, going back to April 19 2016 (though the graphic visualizations are only for the current day).
![](/images/100Days/Day14/history.png)
It seems like this home has a PV panel also and was documenting how much power it generated. And I seemed to be able to uh turn it off? And not only that but I could seemingly do things like... turn off the lights in the house?
![](/images/100Days/Day14/lights.png)
In taking that screenshot I accidentally clicked one of the lightbulbs on. I was suddenly struck with the idea that I'd possibly just woken this person up, since it was the middle of the night in Germany. Needless to say, I decided to stop there. See you tomorrow.

PS here's my traveling `traceroute`, from Cuties Coffee in Los Angeles to Vreden, Germany.
```
👻🌵🔮 $ traceroute 85.190.248.171
traceroute to 85.190.248.171 (85.190.248.171), 64 hops max, 52 byte packets
 1  192.168.0.1 (192.168.0.1)  8.477 ms  3.167 ms  3.413 ms
 2  142.254.182.113 (142.254.182.113)  19.861 ms *  13.392 ms
 3  agg58.lsdwcaro01h.socal.rr.com (24.30.174.233)  13.529 ms  13.357 ms  21.556 ms
 4  agg21.lamrcadq01r.socal.rr.com (72.129.10.192)  17.601 ms  20.589 ms  22.920 ms
 5  agg28.lsancarc01r.socal.rr.com (72.129.9.0)  24.212 ms  28.416 ms  48.527 ms
 6  bu-ether26.lsancarc0yw-bcr00.tbone.rr.com (66.109.3.230)  24.408 ms  23.611 ms  22.001 ms
 7  bu-ether11.tustca4200w-bcr00.tbone.rr.com (66.109.6.5)  21.756 ms  21.032 ms
    bu-ether45.chctilwc00w-bcr00.tbone.rr.com (107.14.19.36)  24.091 ms
 8  4.68.111.101 (4.68.111.101)  18.474 ms  26.681 ms  18.794 ms
 9  * * *
10  ae0-3356.nyk10.core-backbone.com (4.35.80.194)  99.160 ms  102.602 ms  95.709 ms
11  ae3-2072.ams10.core-backbone.com (80.255.15.165)  217.299 ms  164.564 ms  189.938 ms
12  nl.ams01.epcan.de (81.95.15.142)  187.750 ms *  169.762 ms
13  * * *
14  85.190.248.171 (85.190.248.171)  194.505 ms !X  226.705 ms !X  194.739 ms !X
```
