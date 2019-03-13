+++
title = "Shodan Stories Day 68: A Construction Site in Northern Illinois"
date = 2019-03-12T23:32:29-04:00
draft = false
tags = []
categories = ["100 days"]
+++


Busy today so I found an IP camera. This time I got one of my all time favorites, an [AXIS](https://www.axis.com/en-us) camera, this one with [a 4K resolution and 700° pan/tilt control](https://www.axis.com/en-us/products/axis-q6128-e/).

## AXIS Q6128-E Network Camera on 107.85.76.185
Shodan couldn't identify where it was beyond "United States", and I found that was likely because it was connected to the network via a mobile [Sierra AirLink router](https://www.sierrawireless.com/products-and-solutions/routers-gateways/airlink/), the kind we've seen several times now. So my main goal was just to find out where this camera is.
![](/images/100Days/Day68/firstlook.png)
Good start, it's in a construction site and I have pan/tilt/zoom control to look around with. Because it's 4K I can get extremely zoomed in with very high resolution.
![](/images/100Days/Day68/thermostat.png)
This thermostat is on the third-farthest central beam. I can almost make out the temperature, but not quite. But look at that dirt!
![](/images/100Days/Day68/face.png)
I found this thing that looks like a face with teeth on the far wall. Well it kind of looks like a face.
![](/images/100Days/Day68/rockford.png)
After looking around for awhile, finally I found  a tag on one of the pieces of equipment, which read

>Northern Illinois  
>SERVICE  
>Rockford, Illinois  

Aha! [Rockford, Illinois](https://en.wikipedia.org/wiki/Rockford,_Illinois), or at least somewhere close by.

I think we can call this one case closed. See you tomorrow.
