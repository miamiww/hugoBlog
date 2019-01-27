+++
title = "Shodan Stories Day 23: Super Mediocrity in Albuquerque, Wifi Garage Doors, WebIOPi, and the Great Xylophone Saga of 2015"
date = 2019-01-26T11:14:58-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today's was a true delight, a real moment of striking gold, of finding something so beautifully weird that I can barely contain my excitement in writing this. Truly the spice of life, this. I started off wanting to find a wifi connected garage door, and I read that garage door openers are a common application of [WebIOPi](http://webiopi.trouch.com/), which is a toolkit for Raspberry Pis to turn them into common IoT products via their [GPIO pins](https://www.raspberrypi.org/documentation/usage/gpio/). Essentially, the Pi will run a little web app and then you can customize the functionality of the web app to control the GPIO pins in order to run motors, turn lights on and off, open garage doors, etc.

## SuperMediocre on 73.26.38.233
I read that most WebIOPi-running Pis will declare themselves as such, so I just searched on Shodan for "WebIOPi". I had to go through a lot before I found a garage door related one, but I did eventually find one in Albuquerque, New Mexico.
![](/images/100Days/Day23/garage.png)
You don't seem to be able to actually control the garage doors from here. Rather it seems to be recording the status of two garage doors, based on automatically determining the percent open of each door. You can also see the garage doors' open status history and set a PIN, which doesn't seem to impact anything on the page though possibly will make it a little difficult for the door owners to get into their garage in the morning.

I thought that maybe that would be it and that it would be a rather quick day, but I checked the HTML of the page that this Pi was hosting just to see if I could find any clues to how it worked. I found that when you toggled on the "Display Video" box it attempted to stream a video though it appeared that that video was blank. Checking the video source quickly made me forget about the garage doors.
![](/images/100Days/Day23/html.png)
"supermediocre.org"... that's extremely specific! And fairly unusual. I went to it immediately.
![](/images/100Days/Day23/thefamily.png)
Aaaaaaaaaah!!!
![](/images/100Days/Day23/rich.png)
Do you share in my joy in this moment? supermediocre.org is a WordPress blog made by [a man to document building a xylophone with his son](https://www.youtube.com/watch?v=YzSVmsrJEzk). Normally I don't like to publish peoples' names but in the context of a very public-facing blog I think getting your name out is almost the point. In case you were anxious about it, yes they completed the xylophone.
![](/images/100Days/Day23/xylocomplete.png)
Turns out building a xylophone is really hard. The daughter of the family made a little documentary that I watched that went in depth about the process and wow I would not want to do it. Their work was eventually featured in [Popular Mechanics](https://www.popularmechanics.com/) (you can read the full issue that features the xylophone [on the Internet Archive](https://archive.org/stream/Popular_Mechanics_September_2016_USA/Popular_Mechanics_September_2016_USA_djvu.txt)).
![](/images/100Days/Day23/popmech.jpg)

I did find that yes they had a camera observing their garage door and a bit else besides, but let's not worry about that right now. Imagine building your own xylophone. Imagine what you'd need, the resources, the tools, the knowhow, the _time_. Imagine smoking a cigar in your garage, beaming with pride, a pride and joy so overflowing that you decide to make a blog about your family so the whole world can see it.

Most people never get that. See you tomorrow.
