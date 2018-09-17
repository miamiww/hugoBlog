---
author: alden
categories:
- understanding networks
date: 2018-09-10
title: Bad Pong
draft: false
url: /2018/09/10/bad-pong
---
![*ENHANCE.EXE](https://us.123rf.com/450wm/wavebreakmediamicro/wavebreakmediamicro1701/wavebreakmediamicro170110214/70222779-rear-view-of-businessman-in-shirt-waving-against-business-interface.jpg?ver=6)

I really like gesture controls, nothing makes me feel more like a technopagan completing a ritual than controlling something on my screen just by waving my hands around, so I decided that I wanted to control the paddle in just such a manner.
Initially in order to make some kind of gestural control system I wanted to put a camera on a raspberry pi and train it to recognize particular hand shapes, but  that sounded like overkill and I missed the Arduino IDE too much not to take advantage of the opportunity to use it again. So I found my old Node MCU ESP2866 that I bought long before I ever knew how to use it and got working with it. I decided that each hand should control one axis of motion, with the left to right motion seemingly being most important for gameplay and being right handed I decided to have my right hand do left right and left hand do up down. If that sentence is confusing just read it a couple of more times and it will make sense I swear.
![*I actually got quite good](/images/ballgamecontrollerphoto.jpg)
For sensors I used two of my favorite HC-SR04s, and I added an LED as an indicator for connectedness to the game server. For some reason this schematic has the GND and TRG legs of the HC-SR04s swapped, but if you check in the fritzing breadboard file they are labeled correctly.
![*I actually got quite good](/images/ballgamecontroller.png)
Initially I had quite a bit of trouble with getting the game client to work. I found two tactics very helpful: trying to nc localhost from the computer running the game client to check if it's a problem on that end, and also unplugging and plugging in my router. I think my wifi only went down because I was poking around with nmap to make sure I had my ports open (also a helpful tactic).
![*I actually got quite good](/images/badpong.gif)
I ended up getting fairly good at playing the game this way, but the learning curve was steep. There might be a better sweet spot in the settings I made for the HC-SR04s but I didn't find it.
For more info check [project code and details here](https://github.com/miamiww/UndNetworks/tree/master/ballgame)
