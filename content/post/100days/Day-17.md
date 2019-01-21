+++
title = "Shodan Stories Day 17: An ATM in Perm, Russia and Just How Much Market Capture Does Windows 2000 Have Anyway?"
date = 2019-01-20T12:43:31-08:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I thought it might be fun to find an ATM, largely because I wanted to answer the question "why connect an ATM to the internet with a static IP?" I checked for past Shodan searches for ATMs to see if I could find anyone else looking for some so I would know what to look for, and I was able to find someone else looking for ATMs from a brand named [NCR](https://www.ncr.com/), which work over port 169.
![](/images/100Days/Day17/atmncr.png)
So I followed their lead and got looking.


## An NCR ATM on 178.161.141.162
I found quite a few [NCR ATMs](https://www.ncr.com/financial-services/intelligent-deposit-atms), most of which were in Russia, so I picked one of the first Russian ATMs and took a look, and found that Shodan had the output from their UDP scan of this ATM's 169 port.
```
NCR Self-Service Terminal Hardware: x86 Family 15 Model 2
Stepping 9 AT/AT COMPATIBLE - Software: Windows 2000 Version 5.1 (Build 2600 Uniprocessor Free)
```
![](/images/100Days/Day17/NCRpersonas.png)
It seems like NCR has discontinued the 86 line as they were no longer advertising them on their website, instead showcasing their 81, 82, and 88 models. I tried to replicate the scan Shodan had done couldn't figure out how they had gotten that response, finding instead that port 169 on this device was closed.
```
➜  ~ nmap -p 169 178.161.141.162
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-20 18:42 PST
Nmap scan report for 178.161.141.162.ipn.v4.saturn-internet.ru (178.161.141.162)
Host is up (0.28s latency).

PORT    STATE  SERVICE
169/tcp closed send

Nmap done: 1 IP address (1 host up) scanned in 1.03 seconds

➜  ~ nmap 178.161.141.162
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-20 12:57 PST
Nmap scan report for 178.161.141.162.ipn.v4.saturn-internet.ru (178.161.141.162)
Host is up (0.23s latency).
Not shown: 990 closed ports
PORT      STATE    SERVICE
135/tcp   filtered msrpc
139/tcp   filtered netbios-ssn
445/tcp   filtered microsoft-ds
1060/tcp  open     polestar
1098/tcp  open     rmiactivation
9593/tcp  open     cba8
9594/tcp  open     msgsys
9595/tcp  open     pds
33354/tcp open     unknown
52869/tcp filtered unknown

Nmap done: 1 IP address (1 host up) scanned in 31.88 seconds
```
I couldn't totally figure out what these services were doing. [Polestar](https://polestarllp.com/), [Java RMI activation](https://river.apache.org/release-doc/3.0.0/release-notes/activation.html), and [msgsys](https://www.neuber.com/taskmanager/process/msgsys.exe.html) make it seem like it's definitely an enterprise piece of equipment running Windows (as of course so does the microsoft-ds). So Shodan probably isn't lying to me, but possibly something had been changed on the ATM since Shodan had done its scan.

I was able to find the [datasheet](https://ncr.co.il/wp-content/uploads/2014/05/6786.pdf) for the x86 family of NCR ATMs to see if I could find any clues. The datasheet read more like an advertisement really than as a proper datasheet, which I suppose makes sense because you wouldn't want to give too many details away of your ATM system but you do want to turn any eyeballs you get into a sales conversion opportunity.

Well I still couldn't figure out why you'd want to connect an ATM with a static IP. What's the business model there? And what are the risks? Other than people like me poking about the place. See you tomorrow.
