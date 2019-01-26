+++
title = "Shodan Stories Day 22: Raising Cow Fighting Squid in Yilan"
date = 2019-01-25T22:33:00-05:00
draft = false
tags = []
categories = ["100 days"]
+++

I saw someone's search for "Synology DiskStation" and even given our little foray into [Synology](https://www.synology.com/en-us) back on day 20 I was ready to dive back into the world of the globe's premier network attached storage maker.

## A Prototype of a Taiwanese Farm's Website on 114.34.78.222

[The DiskStation promises "personal cloud storage"](https://www.synology.com/en-us/products/DS119j) which to me sounds just like a personal server you connect to the internet, but maybe I'm just old fashioned. It looks like they typically are used just for storing files and having them be remotely accessible or streamable, but that some of the models are capable of hosting web servers as well. Since webservers typically have fun interesting content I thought I'd find a DiskStation with a webserver attached and first one I found like that is in Taiwan.
![](/images/100Days/Day22/fruit.png)
Looking around before using google translate I was able to determine that it was some kind of unfinished website about food with a lot of focus on fish.
![](/images/100Days/Day22/fish.png)
There was a fair bit of content here but then a lot of stock lorem ipsum content.
![](/images/100Days/Day22/fruits.png)
I thought using Google translate would help but it did not.
![](/images/100Days/Day22/translate.png)
Google translate also seemed to be translating what must have been "trout" to "squid". I guess there's still room for humans in the translation pipeline after all.

I did a port scan and saw that port 5000 was also open. I checked it and it was just the remote login for the DiskStation.
![](/images/100Days/Day22/login.png)

Finally I was able to find some contact info nestled in the original page.
![](/images/100Days/Day22/contact.png)
Googling that email address led me to the [Taiwanese government's agriculture homepage](https://www.coa.gov.tw/fpiss/index.php?page=5&category=f), where I was able to find the email address associated with a farm and fishery in [Yilan County](https://en.wikipedia.org/wiki/Yilan_County,_Taiwan).
![](https://eng.taiwan.net.tw/att/1/big_scenic_spots/pic_11548_9.jpg)
Yilan County looks obscenely beautiful, even given the slant of your typical tourist photo set. Grassy cliffs and mountains leading right up to the ocean, valleys with sloping graceful hills, rocky subtropical beaches with palm trees and sawgrass.

Being a farmer there must be a true joy. But why do they have this defunct website sitting around on an at-home server, seemingly since 2013? See you tomorrow.
