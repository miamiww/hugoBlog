+++
title = "Shodan Stories Day 74: Charging My Car in Heraklion"
date = 2019-03-19T10:45:46-04:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I saw a search for "charging station" and I thought I would take a look.

## Electric Car Charging Station on 62.103.74.118
There seemed to be a variety of brands of devices that showed up, but all of them were charging stations for electric cars. I ended up picking one in Greece with no authentication. It was running a webserver on port 10000.
![](/images/100Days/Day74/firstlook.png)
I love this. It's a dashboard for an electric vehicle charging station made by [Etrel](http://etrel.com/), a Slovenian maker of such charging stations (here's the [manual](https://www.zielony-dom.pl/wp-content/uploads/2019/03/Etrel-INCH-User-manual-EN.pdf)).
![](https://www.phytec.eu/fileadmin/user_upload/images/content/2.Projects/ETREL-charging-station.jpg)
They look slick. Very modern. Unfortunately not very secure, as the default is to have no password on the web interface.
![](/images/100Days/Day74/settings.png)
I could add my own password, or change the maximum current of the charger. Most interestingly for me I could see the usage history in kWh.
![](/images/100Days/Day74/recentuse.png)
That's pretty low. Like barely anything low. According to a [guide I read](https://www.greencarreports.com/news/1082737_electric-car-efficiency-forget-mpge-it-should-be-miles-kwh) the average electric car uses about 3.4 kWh per mile. So that means that the roughly .15 kWh/day this charger has been using in the past week is likely just the "vampire draw" of having the vehicle plugged in without any real use.
![](/images/100Days/Day74/2018.png)
Looking at the annual usage it seemed like the vehicle probably hadn't been used since April 2018. Before that it was showing usage (with quite a few spikes and then seeming non-use) since 2016.

Since it is on Crete, an island in the Mediterranean, there aren't particularly large distances to travel, so I understand the light and inconsistent usage. Seems a little strange though. See you tomorrow.
