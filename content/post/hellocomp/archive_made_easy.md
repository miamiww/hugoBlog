+++
title = "Archives Made Easy"
date = 2018-09-24T17:22:44-04:00
draft = false
tags = []
categories = ["hello computer"]
+++

Recently I've been reading a ton of books with names like "Cyber Dictionary: Your Guide To The Wired World" or "Net Chick: A Smart-Girl Guide to the Wired World", hip and breezy internet guide books written between 1996-2000.
![*netchick](https://images-na.ssl-images-amazon.com/images/I/51y-zHzeoZL._SX419_BO1,204,203,200_.jpg)
This has led to me making a few strange archive tools around the Internet Archive's [Wayback Machine](https://archive.org/web/)

The one I made for Hello Computer this week, a voice controlled archive navigation system, can be found [here](http://arj247.itp.io/archive) but unfortunately because I don't have HTTPS certification on my prototypes site Chrome will not allow you to access the microphone, so all you can see is the initial button. If you click that button and say something you'll see the following:
![](/images/HelloComp/interface.png)
The "click me" button will take you to the first instance of a url based on whatever you said that is in the archive. So, if you said "data" for example, you would get the lovely www.data.com of yesteryear.
![](/images/HelloComp/data.png)
The interface is very basic for testing functionality, ideally I would gussy it up a bit with some web 1.0 graphic stylings. Maybe an "under construction" gif or two.
I didn't have time to set up [Let's Encrypt](https://letsencrypt.org/) this week but maybe some day... I should get it on my main page also although I really have no reason to other than Chrome flags it as "insecure".
Code and whatnot [here](https://github.com/miamiww/HelloComputer/tree/master/talk_at_me). I make use of the [Wayback Machine API NPM package](https://www.npmjs.com/package/wayback-machine) and [socket.io](https://socket.io/).
