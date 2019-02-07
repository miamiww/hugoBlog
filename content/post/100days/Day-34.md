+++
title = "Shodan Stories Day 34: Listening to La Merde in Bonneuil-sur-marne, Logitech Servers, the Squeezebox, and Becoming the Ghost in the Wifi Connected Radio"
date = 2019-02-06T01:21:02-05:00
draft = false
tags = []
categories = ["100 days"]
+++

As many of my days now start, I began my morning by looking through the recent searches on Shodan. I found one for [Logitech devices](https://www.logitech.com/en-us) that looked kind of interesting and dove in.

## Logitech Media Server on 82.64.23.201
I no longer remember why I picked this particular device since I did my searching in the morning and am writing at night. I think I was impressed by the number of ports it had open. Maybe I was interested because it is in a [Paris suburb](https://en.wikipedia.org/wiki/Bonneuil-sur-Marne). Shodan indicated that it had a Logitech device running a web server on port 9000, but had several other ports open with different types of services.
![](/images/100Days/Day34/firstlook.png)
I opened up port 9000 in my browser and gave myself a couple of seconds to figure out what I was seeing. Clearly it was a media server of some kind. After poking around a bit I realized that it was just for audio! Phew no more porn.
![](/images/100Days/Day34/genres.png)
The owner had about 45000 tracks on the server, with all the usual genres. I think I had about that many back at the height of my torrenting teen years.
![](/images/100Days/Day34/merde.png)
I found that I could download any of the mp3s, but couldn't steam them even though there were little "play" buttons next to all of them. I downloaded this album by a bizarre Fench comedy musician [Didier Super](https://fr.wikipedia.org/wiki/Didier_Super). It was a cover album of French pop classics. It was really bad. Reading about it I found that he just made it to fulfill a four album contract, which might explain the bad music and pretty gross cover art.

I decided to Google the big word in the upper right corner, "Squeezebox".
![](/images/100Days/Day34/squeezebox.png)
Uh oh! Had I just been playing tracks on someone's Wifi radio?? What time was it there? Breathing a sigh of relief as I realized it was in the middle of the day - hopefully the owner was out. If an internet-connected radio starts randomly playing tracks in an empty apartment does it make a sound?


Googling a little further [I found a guide for how to set up port forwarding for these devices](http://wiki.slimdevices.com/index.php/Connecting_remotely) although it _strongly_ advised not to.
![](/images/100Days/Day34/softsqueeze.png)
Looking a little deeper on the web app though I found that it was running something called [SoftSqueeze](http://softsqueeze.sourceforge.net/) - which is actually an emulator for the Squeezebox firmware to run on any kind of common consumer level computer.

I decided to do an `nmap` to get a feel for what else is going on.
```
➜  ~ nmap -p- 82.64.23.201
Starting Nmap 7.70 ( https://nmap.org ) at 2019-02-06 01:26 EST
Nmap scan report for sub-82-64-23-201.proxad.net (82.64.23.201)
Host is up (0.19s latency).
Not shown: 65517 filtered ports
PORT      STATE  SERVICE
80/tcp    open   http
443/tcp   open   https
554/tcp   open   rtsp
1935/tcp  open   rtmp
3483/tcp  open   slim-devices
8000/tcp  open   http-alt
8080/tcp  open   http-proxy
8125/tcp  open   unknown
8210/tcp  open   unknown
8215/tcp  open   unknown
8220/tcp  open   unknown
8221/tcp  closed unknown
8222/tcp  closed unknown
8224/tcp  open   unknown
9000/tcp  open   cslistener
15567/tcp open   unknown
20040/tcp open   unknown
25320/tcp open   unknown

Nmap done: 1 IP address (1 host up) scanned in 449.77 seconds
```
![](/images/100Days/Day34/reolink.png)
The 80/443 webservers were running a login for something called [Reolink](https://reolink.com), which seems to be some kind of home surveillance/ip camera system. Port 554 was running a real time streaming application, which I thought was maybe the surveillance cams, but I couldn't login to it (though I did confirm that it was streaming video). The port 1935 was [another media stream](https://en.wikipedia.org/wiki/Real-Time_Messaging_Protocol). 8000 was some kind of [SOAP](https://en.wikipedia.org/wiki/SOAP) service (we'll get back to 3483 in a second).

![](/images/100Days/Day34/rancher.png)
8080 was running a login for [Rancher](https://rancher.com/), which is a service for running multiple clusters of [Kubernetes containers](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/). At some point I want to spend a day diving into containers, but today is not that day. Suffice it to say that this raised a lot of questions for me that I was unable to answer.

All the other ports were impenetrable. Back to 3848, I read on the guide to setting up port forwarding for you Squeezebox that you would need to forward both ports 3848 and 9000 because the Squeezebox uses both of them. The [IANA port registry](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml) that `nmap` uses says that that port is for 'slim-devices', not 'squeezeboxes', so I looked it up. It turns out that [Slim Devices](https://en.wikipedia.org/wiki/Slim_Devices) was the name of the company that first made the Squeezebox way back in 2001, before it was acquired by Logitech in 2006.

Why does IANA still have ports named after companies and services that haven't been around in over 10 years? See you tomorrow.
