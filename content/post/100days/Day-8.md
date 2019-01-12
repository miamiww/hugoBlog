+++
title = "Shodan Stories Day 8: Mining Ethereum in Caracas, AMD GPUs, and Taking a Dip in the Nanopool"
date = 2019-01-11T16:55:45-05:00
draft = false
tags = []
categories = ["100 days"]
+++

A couple of days ago I noticed some people searching on Shodan for "ETH: total speed". That didn't mean anything to me so I took note of it and today decided to dig in.


## An Ethereum Miner on 186.90.40.229
Almost all the results I found for this search in Shodan were running off of port 3001 (the ones that weren't were on 9001), and tended to be in Russia, South Korea, or Ukraine. I chose one of the first IPs I found, this one from Caracas in Venezuela. I was initially pretty confused by what I was looking at when visiting it in a browser.
![](/images/100Days/Day8/ETH1.png)
What exactly is going on here? It looks like terminal output, but in a browser. Someone is tracking speeds of their 11 Radeon GPUs for discreet jobs, but even after googling "ETH: total speed" it wasn't totaly clear to me what I was seeing. This server had two other ports open: 2021 and 2022, but each of those just prompted logins when I tried to visit them.
```
➜  sandbox git:(master) ✗ nmap 186.90.40.229 -Pn
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-11 17:00 EST
Nmap scan report for 186-90-40-229.genericrev.cantv.net (186.90.40.229)
Host is up (0.23s latency).
Not shown: 997 filtered ports
PORT     STATE SERVICE
2021/tcp open  servexec
2022/tcp open  down
3001/tcp open  nessus

Nmap done: 1 IP address (1 host up) scanned in 31.90 seconds
```
![](/images/100Days/Day8/login.png)

The main clue is the line
```
New job from eth-us-west1.nanopool.org:9999
```
![](/images/100Days/Day8/nanopool.png)
Visiting nanopool.org it was suddenly so clear: ethereum mining! _of course!_ After [reading a guide](https://blockonomi.com/how-to-dual-mine-ethereum-and-sia/) about how to mine Ethereum it seems like miners join resource pools like nanopool in order to share their GPUs for greater overall reward, with only a small payout (1%) to the pool itself. And some of the [mining software on nanopool's github](https://github.com/nanopool) had output screenshots that look just like the output I was seeing from my IP, meaning that it is likely running some of nanopool's mining software.
![](/images/100Days/Day8/nanopool2.png)
It seems like nanopool has quite the operation, with 44,226 miners, of which I had only found one.

One last point that is interesting here: from `nmap` I saw that the IP is registered under 186-90-40-229.genericrev.cantv.net. [CANTV](http://cantv.net/) is the [nationalized internet service of the Venezuelan government](https://en.wikipedia.org/wiki/CANTV). I tried to find if they were offering any cloud computing services, but I couldn't tell, meaning that this IP is probably connected to somebody's home, running a machine with 11 GPUs. That makes sense, since the costs of mining off of virtual machines might be prohibitive, unless nationalized internet costs are just that cheap.

But why AMD GPUs and not Nvidia? And how does this kind of pooling work? See you tomorrow.
