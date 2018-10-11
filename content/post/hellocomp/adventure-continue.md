+++
title = "Adventure Continue"
date = 2018-10-09T17:52:12-04:00
draft = false
tags = []
categories = ["hello computer"]
+++

I tried to continue on my theme of making a colossal cave adventure clone for voice, thinking that this time using the webhook fulfillment it would be much clearer what to do. I did get it functioning, somewhat.
![](/images/HelloComp/adventure_south.png)
Unfortunately going south here should get you into the forest. I encountered numerous other bugs, such as items not appearing in the rooms they should be in, and getting stuck in a room permanently. Also I noticed that whenever I quit the game and restarted it, it would start in the room I had left in. Curious...

You can see all of the code [here](https://github.com/miamiww/HelloComputer/tree/master/talk_adventure). I think the last issue is because I used global variables to set up the "current room", which I have reset when I 'quit' properly, but that won't reset if I just exit out of the test window. I think really I should be using a "world-object" or something of the like, that keeps track of all the 'rooms', their states, geographic relationship to each other, and what they have in them. But that doesn't answer to me why you can get stuck in a room, and debugging on DialogFlow is a bit of a pain.
