+++
title = "Shodan Stories Day 9: I Got Rickrolled by an Irrigation System in Los Vegas"
date = 2019-01-12T20:30:45-05:00
draft = false
tags = []
categories = ["100 days"]
+++

This is another one I found from looking at recent searches on Shodan. Someone searched for "BlueSpray irrigation" and I decided to follow their lead.

## BlueSpray Wifi-Enabled Irrigation Controller (or maybe somebody's pentesting playground) on 71.52.48.61
[BlueSpray](https://www.bluespray.net/#home) is a startup that makes an internet of things irrigation system for the consumer level (so for suburban lawns, not farms). If "internet of things lawn sprinkler" makes your eyes roll all the way back into your head well then this blog is for you. If however you feel like your current lawn watering system is leaving you high and dry and you'd like the ease and convenience of lawn monitoring from anywhere and by anyone you can get started with BlueSpray by buying their [controller, only $250 on Amazon](https://www.amazon.com/BlueSpray-Zone-Wi-Fi-Watering-Control/dp/B00E7V8SSY/ref=pd_rhf_se_p_tnr_1).
![](https://www.bluespray.net/images/connected.png)
Reading BlueSpray's website I noticed a couple of interesting things. The first is a [blogpost from 2015](https://bluespray.net/blogs/?p=59) saying that in their newest firmware update they enabled static IPs for their devices. The second is this great advice that a lot of people out there don't seem to fully follow:
![](/images/100Days/Day9/advice.png)
One of the first results I found for "BlueSpray" on Shodan was in Los Vegas, and I decided to look at that one because "lawn watering in Los Vegas" sounded to me like a great name for a third wave ska album.
Visiting the device's IP in my browser (Shodan indicated that I should check port 8000, not the usual 80), I was, shall we say, surprised in a negative way.
![](/images/100Days/Day9/RickRolled2.png)
If you don't immediately recognize the man in the picture, that is Rick Astley, mostly famous to me because of [RickRolling](https://en.wikipedia.org/wiki/Rickrolling), the [horrible meme of yesteryear](https://www.youtube.com/watch?v=dQw4w9WgXcQ).
I had two immediate thoughts. First: I had clearly been RickRolled. It's been years, and I admit this with shame. The second: some Shodan hacker had gotten here first and replaced someone's lawn image with Rick Astley. BlueSpray lets you add your own lawn image and here they had just put in a direct to a picture of Rick.
![](/images/100Days/Day9/source.png)
I looked around and found that I could probably futz with this lawn's water scheduling. I also found their watering history since last August. They didn't do any watering in December or January, maybe because of the winter. They had watering scheduled starting in February, starting with once a week, then moving to three times a week in spring and five times a week in summer.
![](/images/100Days/Day9/HistoricalData2.png)
However my second conclusion started to break down when I used `nmap` on the IP.
```
➜  sandbox git:(master) ✗ nmap -p- 71.52.48.61
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-12 16:38 EST
Nmap scan report for 71-52-48-61.lsv2.centurylink.net (71.52.48.61)
Host is up (0.096s latency).
Not shown: 65520 filtered ports
PORT      STATE  SERVICE
443/tcp   open   https
2101/tcp  open   rtcm-sc104
2106/tcp  closed ekshell
7080/tcp  open   empowerid
7443/tcp  open   oracleas-https
7445/tcp  open   unknown
7446/tcp  open   unknown
7447/tcp  open   unknown
8000/tcp  open   http-alt
8080/tcp  open   http-proxy
8090/tcp  open   opsmessaging
8091/tcp  open   jamlink
8443/tcp  open   https-alt
9443/tcp  open   tungsten-https
18922/tcp open   unknown

Nmap done: 1 IP address (1 host up) scanned in 262.49 seconds
```
That's a lot of ports open running a lot of services. And probing all of them in the browser yielded another theory.

Checking the IP via 443 (just https, and yes Chrome gave me a warning that they didn't have a certificate) shows the login for a service called [UniFi Video](https://www.ubnt.com/unifi-video/unifi-nvr/), which is a service run by [Ubiquiti Networks](https://video.ubnt.com/) and promised to be an internet of things total surveillance solution. Port 7080 shows the same thing.
![](/images/100Days/Day9/unify443.png)
Port 8080 in a browser shows a login for [Universal Devices](https://www.universal-devices.com/), which makes iot products for home automation.
![](/images/100Days/Day9/unidevices.png)
Port 8090 shows a login for a surveillance IP camera manufactured by [Foscam](https://www.foscam.com/).
![](/images/100Days/Day9/foscam.png)
Port 8091 shows a login for something that I can't identify.
![](/images/100Days/Day9/8091.png)
And 18922 actually redirects to a login for app.plex.tv, which looks like some kind of [media storage system that lets you watch your .avi movies from anywhere you want](https://www.plex.tv/).
![](/images/100Days/Day9/Plex.png)
All the other ports that were open gave back my browser an empty response.


Did I just stumble onto someone's IoT fortress with a ton of port forwarding? Or is this someone's phishing scam to collect logins? Or is this someone's test server for penetration testing a bunch of different IoT services? Or was this all an elaborate honeypot set up to rickroll hackers? I can't figure it out, but it definitely seems off. Weird that it looked like there was actual irrigation history in the sprinkler though. See you tomorrow.
