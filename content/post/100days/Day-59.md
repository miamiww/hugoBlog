+++
title = "Shodan Stories Day 59: High Precision Instruments in Bosnia and Herzegovina, Leica Geosystems Satellite Receivers, and Our Story of 80 Years of Mergers and Acquisitions"
date = 2019-03-03T16:42:04-05:00
draft = false
tags = []
categories = ["100 days"]
+++

A plethora of good shared searches on Shodan today. I decided to go with satellite receiver web interfaces, thinking that after my attempts back on day 13 this would be about as close to a real satellite as I could get.

## Leica Satellite Receiver on 212.39.114.78
I chose a result in Bosnia and Herzegovina. It was running email ports and a webserver on port 80, so I took a look at the webserver.
![](/images/100Days/Day59/firstlook.png)
Ah yes the _Leica GRX1200+ GNSS_. So fun! It connects to [GPS](https://en.wikipedia.org/wiki/Global_Positioning_System), [GLONASS](https://beebom.com/what-is-glonass-and-how-it-is-different-from-gps/), and [GALILEO](https://en.wikipedia.org/wiki/Galileo_(satellite_navigation)) satellite location services. It's a device for [extremely accurate location data acquisition and logging](http://www.geotech.sk/OLD/t7_GRX1200en.pdf). And it's pretty expensive!
[![](/images/100Days/Day59/expense.png)](https://www.precision-geosystems.com/product/leica-grx1200-gnss-pro-gpsglonass-reference-station-ethernet-enabled/?v=7516fd43adaa)
[Leica Geosystems](https://en.wikipedia.org/wiki/Leica_Geosystems) has a reputation for making very high quality devices. I was trying to figure out their corporate history though, and it twists and turns from owner to owner and brand to brand. They used to be known as Wild Heerbrugg until they were taken over by Leica of the [camera fame](https://en.wikipedia.org/wiki/Leica_Camera), which actually leases the name Leica from the former subsidiary [Leica Microsystems](https://en.wikipedia.org/wiki/Leica_Microsystems). That's barely a fifth of the confusing story of this company. Where has there been so much corporate turmoil in this particular cottage industry?

Unlike a lot of devices that leave their web interfaces open online, this one has all of the configuration pages locked by a password. But all of the logging metadata and position data are available unauthorized. Which means... yes and I hope you're as excited as I am, we get the exact position of the device!!
![](/images/100Days/Day59/position.png)
Amazing. That means we can find it on Google maps.
![](/images/100Days/Day59/building.png)
And here it is, the GRX1200 is in this building. But why?

ENHANCE
![](/images/100Days/Day59/enhance.png)
I can't really imagine why it's here. It looks like a normal apartment building, albeit one with a store named SPORT REALITY on the first floor. I wish I could get a view of the roof to see if there is any kind of station on top.

But oh well, maybe someone just has it in their apartment. See you tomorrow.
