+++
title = "Shodan Stories Day 44: Dealing with the Devil in Quebec, Repetitive Jetpack Death, Dr. Cheetos' Pain Chamber, Ludum Dare 43, Unity Web GL, and What Happened to Dave?"
date = 2019-02-16T20:51:47-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Saw a great search today, this for [Unity Engine Web Players](https://unity3d.com/). Unity is a hugely popular 3D game engine, primarily used for making video games but has a wide range of applications, including workflow simulation, architectural prototyping, and filmmaking. Typically Unity outputs run as stand alone applications, but it also has the ability to output applications for the web via [Web GL](https://en.wikipedia.org/wiki/WebGL).

## Unity Web GL on 52.15.155.102
There were about 600 results for this search and I picked the first result I found. It was just running an HTTPS webserver on 443.
![](/images/100Days/Day44/firstlook.png)
Cute! It's a seemingly really simple game called "Project Jetpack". You have to navigate a little jetpack-wearing person through a bunch of planks all floating in space. Touching anything but the safe beginning and ending pads yields a gratuitous and immediate death.
![](/images/100Days/Day44/level2die.png)
I ended up getting to about level 8 or 9 but it got too hard for me once the planks started moving all over the place. I died many many times along the way with my little Lego-esque avatar spewing heaps of pixelated blood.

I could see from `host` that this was an [Amazon EC2 instance](https://aws.amazon.com/ec2/), and I assumed that someone in the middle of developing this game put it up there to quickly make it accessible for "user testing".
```
➜  ~ host 52.15.155.102
102.155.15.52.in-addr.arpa domain name pointer ec2-52-15-155-102.us-east-2.compute.amazonaws.com.
```

Checking the SSL certificate revealed something interesting.
![](/images/100Days/Day44/https.png)
"drcheetos.hopto.org", an extremely legit url, doesn't seem to exist as a web page. "hopto.org" is the page for a business that allows you to have a dynamic IP address connected to a URL of the structure _myurl_.hopto.org.
![](/images/100Days/Day44/hopto.png)
So clearly Dr Cheetos had been a customer of theirs and likely reused an old SSL certificate for their Amazon EC2 server.

Dr Cheetos was not hard to track down.
![](/images/100Days/Day44/ludumdare.png)
They have a profile on [Ludum Dare](https://ldjam.com/), perhaps the most storied and famous [game jam](https://en.wikipedia.org/wiki/Game_jam) competitions in the world. They participated in the 43rd game jam, not with Project Jetpack, but with a game called My Little Daily Sacrifice.
![](/images/100Days/Day44/mydailysacrifice.png)
![](/images/100Days/Day44/mydailysacrifice2.png)
It's a management-type game where you have to hire people for your company so that you can uh sacrifice them and hand their soul over to satan, all while trying to get enough money together to hire a lawyer to wrangle you out of this raw deal. Satan seems to demand about one soul a day on average so it's a lot of turnover. All your little cute pixel graphics employees sit at their desks making you money but when you sacrifice an employee their physical body is turned into a puff of black smoke as satan drags their eternal soul down to hell for eons of unimaginable suffering and torment. Talk about a case of the Mondays! None of the other employees ever seem to notice anything happening or worry about their cubicle neighbors being blinked out of existence. Seemingly the only consequence is that the murdered employee doesn't make you any money anymore so you'll need to hire someone new to keep profits moving.

I guess in this economy you take whatever job you can get. See you tomorrow.
