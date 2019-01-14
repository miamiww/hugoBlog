+++
title = "Shodan Stories Day 10: Reading License Plates in Louisiana, the Bygone Days of Java Webapps, and Spying on Cops"
date = 2019-01-13T20:08:21-05:00
draft = false
tags = []
categories = ["100 days"]
+++

I was feeling listless today and a bit grumpy, so I decided to look for something that I could be motivationally upset about: [automatic license plate readers (ALPRs)](https://www.eff.org/pages/automated-license-plate-readers-alpr). These are a kind of surveillance camera that are frequently used by police forces or parking facility managers to track cars and car movement. You might have seen a kind of them attached to traffic signal beams to catch red light runners, but they are used far more widely than just that. There's one in just about every police car and on many street corners, you could even [buy your own to put wherever you wanted](https://www.a1securitycameras.com/license-plate-recognition-cameras/). Checking on one of Shodan's explore guides I saw that one major vendor of ALPRs was named [PIPS](http://www.pipstechnology.com/), so I searched for PIPS ALPR.

## An Automatic License Plate Reader on 166.150.87.204
I only found one result. What I had read on Shodan seemed to indicate that there used to be a whole lot of them visible, so maybe they got better at their security and made them less discoverable. The one that I did find seemed to be using an outdated system, since the PIPS logo appeared to be an old version (which looks suspiciously like [Amazon's old logo](https://cms.qz.com/wp-content/uploads/2016/07/screen-shot-2016-07-18-at-10-05-33-am.png?w=1240&strip=all&quality=75)) and the copyright was for 2006. I was able to access it via browser on port 8083.
![](/images/100Days/Day10/Pips.png)
I first tried to see if I could "see through the camera". There was an option for that but unfortunately it was running in a java applet and modern browsers don't allow java plugins. This thing really was old!
![](/images/100Days/Day10/java.png)
Finding a version of a browser that would let me install java wasn't really worth it to me, so I kept looking around. I found some details on the system pretty quickly. Interesting that it seemed to be in Louisiana (I believe what it's talking about in that line below is that it's using a Louisiana license plate database), as Shodan couldn't tell me where the IP was located beyond the United States.
![](/images/100Days/Day10/stats.png)
Checking on a slideshare deck about the PIPS 372 from 2009 I was able to find a little bit more about this specific camera model. It appears that PIPS no long manufactures the 372 (the oldest model they still advertise is the [much sleeker 392+](http://www.pipstechnology.com/fixedalpr/)), but you can buy a used [government surplus one on the cheap](https://www.govdeals.com/index.cfm?fa=Main.Item&itemID=2898&acctID=8445).
![](https://image.slidesharecdn.com/fwindowsvistapresentamarcopipspipspresentation-maprimaq-espanol-090626180417-phpapp01/95/pips-control-de-vehiculos-9-728.jpg?cb=1246041898)
I tried to downloaded all of the recorded pictures but got a 700 error, but also I noticed that I would intermittently be unable to connect anymore, and generally navigating around the system was extremely slow. Another weird thing - each time I checked it with `nmap` it would show me something slightly different.
```
➜  sandbox git:(master) ✗ nmap 166.150.87.204 -Pn
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-13 21:07 EST
Nmap scan report for 204.sub-166-150-87.myvzw.com (166.150.87.204)
Host is up (0.10s latency).
Not shown: 997 filtered ports
PORT     STATE SERVICE
8082/tcp open  blackice-alerts
8085/tcp open  unknown
8088/tcp open  radan-http

Nmap done: 1 IP address (1 host up) scanned in 28.18 seconds
```
And then just a few minutes later:
```
➜  sandbox git:(master) ✗ nmap 166.150.87.204 -Pn
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-13 21:39 EST
Stats: 0:01:16 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 86.05% done; ETC: 21:40 (0:00:12 remaining)
Nmap scan report for 204.sub-166-150-87.myvzw.com (166.150.87.204)
Host is up (0.100s latency).
Not shown: 997 filtered ports
PORT     STATE SERVICE
8081/tcp open  blackice-icecap
8083/tcp open  us-srv
8084/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 126.82 seconds
```
This kind of thing is the reason I grind my teeth at night so much. Just why?? I think part of the reason has to do with the reverse DNS: yadayada.myvzw.com. After looking at it, myvzw.com seems to reference the Verizon Wireless mobile customer network. And so I could occasionally be losing connection because this camera system is on a bad mobile hotspot. Why are the ports showing inconsistently (and occasionally telling me that the host is up but that all ports are filtered, which I know isn't true because I'm looking at it on 8083)?

I was able to download the camera's event log, and all I was able to discern from it was that it had been rebooted about a half dozen times in the past couple of days. Maybe it's just kind of janky? It is pretty old in the world of computational devices. Another possibility is that the BlackICE service, which is a ([now very outdated and no longer used](https://www.itprotoday.com/compute-engines/blackice)) service designed to prevent intrusion attempts, running on 8081 is recognizing me as an intruder. I did `nmap` it a half dozen times after all. See you tomorrow.
