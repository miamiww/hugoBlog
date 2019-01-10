+++
title = "Shodan Stories Day 4: Television in Spain, Firmware Hacking in Palestine, Linux Kernels, Clone Bombs, and 14 Years of Passion"
date = 2019-01-07T12:08:21-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I saw that the fifth most searched for term on Shodan of the day was "dreambox". What a name! I couldn't resist! After a little digging I found that dreambox probably referred to a [kind of linux-based  television receiver](https://en.wikipedia.org/wiki/Dreambox), made by a German company with a truly fantastic logo.
![](https://upload.wikimedia.org/wikipedia/en/1/1b/Drem-multimedia-logo.png)
### Cloned Dreambox Television Receiver on 84.39.177.219
I started out just searching on Shodan for "dreambox", like so many others were doing today. It seemed like the most results were from Spain so I picked a Spanish IP and got to work with `nmap`.

```
👻🌵✨$ nmap 84.39.177.219
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-07 14:40 EST
Nmap scan report for static.masmovil.com (84.39.177.219)
Host is up (0.14s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE
21/tcp   open  ftp
23/tcp   open  telnet
80/tcp   open  http
8181/tcp open  intermapper

Nmap done: 1 IP address (1 host up) scanned in 10.89 seconds
```
Several interesting points: telnet was open and ftp were open!, port 80 was open so it was open to being used by a browser, and it resolves to static.masmovil.com. Looking into [Masmovil](https://www.masmovil.es/) it seems like it's a popular provider of internet service in Spain, so the static probably referring to their static IP range that they would sell to customers. So the owner of this Dreambox probably bought a static IP for it from this stock photo hipster.
![](/images/100Days/Day4/masmovil.png)
I tried connecting using an ftp client, but got refused without a password, then I tried to go to it via browser. Boring log in screen, the same on 8181.
![](/images/100Days/Day4/login.png)
[Netcatting](https://en.wikipedia.org/wiki/Netcat) into port 21 gets a great response of `220 Willkomen auf Ihrer Dreambox`. Makes sense, Dreambox is made by a German company. Netcatting into the telnet port though...
```
👻🌵✨$ nc 84.39.177.219 23
!
***************************
*                         *
*   The Gemini Project    *
*                         *
***************************
*   Prepared By "drhg"    *
*  ( Dream-Gaza Team )    *
*   www.dreamgaza.com     *
***************************

Checking Kernel, Please Wait ....

Kernel 2.6.9.
md5sum (dreambox Linux ppc ).
head.ko = 308509 bytes.
Safe, NO 'clone bomb' found ... Congratulations.

Enjoy Original Gemini Project  without Time Bomb !.
---------------------------------------------------

(Monday, 07 January 2019).
welcome on your dreambox! - Kernel 2.6.9 (18:30:25).


dreambox login:
Login timed out after 60 seconds.
```
Looking at this gave me vertigo, I was staring at the Kantian sublime of my vast unknowing. "The Gemini Project"??? Dream Gaza??? "drhg"??? "clone bomb"??!?! "Time Bomb"?????
I've now figured it all out but gosh what a story.

#### Dream Gaza

I wouldn't recommend going to www.dreamgaza.com now, it redirects you to a malware site that could probably fill out a blog entry of its own.
But checking for it on [The Internet Archive's Wayback Machine](https://archive.org/web/) I found that from 2006 to 2013 it was a [forum for Palestinian Dreambox enthusiasts](https://web.archive.org/web/20120921235706/http://www.dreamgaza.com:80/vb/) who liked to tinker with their machine's linux-based firmware.
![](/images/100Days/Day4/dreamgaza.png)
At their height they had about 60,000 members total, but it seemed like active membership spiked in 2008 and then slowly declined over the next couple of years. They talked about Islamic books, Palestinian news, 3D rendering technology, sports (there were a lot of [FC Barcelona](https://en.wikipedia.org/wiki/FC_Barcelona) fans), space exploration, satellites' hardware, birdwatching, but mostly they talked about what brought them together: linux, Dreambox firmware, and the TV that they watched with their hacked Dreamboxes. They would also share downloads of TV shows they recorded with their Dreamboxes, which seems to be one of the reasons for hacking the Dreambox in the first place. I wish I could read Arabic because Google translate is a little iffy, but it seems like they had a great community.



#### The Gemini Project
![](/images/100Days/Day4/GeminiProject.png)
[The Gemini Project](http://blue-panel.com) was a group of linux hackers who [made and distributed](http://wiki.blue-panel.com) their own Dreambox firmware.
![](/images/100Days/Day4/IHaveADreambox.png)
14 years of passion... I got emotional thinking about it. Suddenly I felt the wound of proprietary closed systems, there's no communities forming around hacking your Amazon Echo, no joy in tinkering with your iPhone's operating system, no feeling of ownership of or passion for your tool. At least that I know of! Maybe I'll find some.

So I have some answers: this machine I connected to was running a version of the Dreambox firmware that had been made by the Gemini Project, which had then been futzed with by the users of the Dream Gaza forum.


#### The Clone Bomb
But why this firmware, in 2019, so many years since Dream Gaza has existed? I had three clues.

1. The [Dreambox Wikipedia article section on "clones"](https://en.wikipedia.org/wiki/Dreambox#Clones)  mentions that _"In April 2008, Dream Multimedia allegedly introduced a time bomb into their latest flash to disable the boot loader on counterfeit models. An unofficial firmware group called Gemini who used the latest flash drivers in their firmware, found that flash corruption would be caused on clone DM500-S receivers"_.
2. The activity on Dream Gaza spiked hugely in mid 2008.
3. A [post on a satellite TV enthusiasts forum from April 2008](https://www.rdi-board.com/forum/rdi-international/rdi-english/67719-warning-dreambox-clone-users)

![](/images/100Days/Day4/clones.png)
As far as I can tell, Dream Multimedia knew that users were out there copying their firmware and loading it onto fake Dreamboxes, which people call "clones", so they put in a clone/time bomb into their firmware release in 2008 that would break the firmware if it were loaded onto one of these clones. The Gemini Group didn't take out the bomb in their release of the firmware for whatever reason, so members of the Dream Gaza forum took out the bomb and put in kernel check that always runs on login to see if there is a bomb in that version of the firmware. This led a lot of people to go to the forum in mid 2008 to get that version of the firmware that has the kernel bomb check. And that firmware version is what this person in Spain is using, 10 years later.

I wonder what they're watching. See you tomorrow.
