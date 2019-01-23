+++
title = "Shodan Stories Day 19: Never Trust Me With The WiFi"
date = 2019-01-22T22:59:41-08:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I'm staying with a friend whose partner has a pretty serious media server set up (with 64TB! of content), and I thought I'd take a look to see if I could find it on Shodan. And sure enough I could!

## My Friend's Media Server on 104.172.240.189
So I had previously seen a [Plex](https://www.plex.tv/) service running on an IP back on day 9, but I didn't investigate it too much because at the time I was focused on the irrigation system. When my friend was telling me about his setup it took quite a while to put two and two together and to realize that I had previously seen this service. [Plex servers](https://en.wikipedia.org/wiki/Plex_(software)) are typically run on port 32400, and require an account and login to access, as Plex ties each individual server back to its own service via a client ID that it connects to when you visit the server's port in the browser. He gave me a pretty decent explanation but I still didn't fully follow how it both exists as a streaming web service and as the software for a self-hosted media server. Seems like a weird business model. But at least I got to see one in the flesh.

I did a port scan and did pen test everything (no vulnerabilities), but realized I felt a little too weird talking about everything on his network since I was able to verify it all by being on the network myself. It's one thing to make guesses about strangers, it's another to list all the things you see in your friend's house.

That being said here are the results of `nmap`. You can see the media server down at 32400. Most everything else I was able to tie to something I saw on the network.

```
👻🌵🔮 $ nmap -p- 104.172.240.189
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-23 00:44 PST
Nmap scan report for cpe-104-172-240-189.socal.res.rr.com (104.172.240.189)
Host is up (0.030s latency).
Not shown: 65528 closed ports
PORT      STATE SERVICE
548/tcp   open  afp
631/tcp   open  ipp
8200/tcp  open  trivnet1
20005/tcp open  btx
28392/tcp open  unknown
32400/tcp open  plex
33344/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 6.18 seconds
```

Please don't hack my friend. See you tomorrow.
