+++
title = "Shodan Stories Day 49: Solving Crimes and Protecting the Innocent in Paris"
date = 2019-02-21T22:23:45-08:00
draft = false
tags = []
categories = ["100 days"]
+++

Another boring day on the shared searches. I decided to search for IPs with "dev environment" in the title, hoping to find something good.

## Ace Attorney Online on 163.172.128.52
Many of the results were pretty interesting and I think it's a fruitful search overall, but one result in France stood out to me.
![](/images/100Days/Day49/firstlook.png)
It's the "developer environment" for a webpage running on port 8080 dedicated to fan-made versions of the popular [Ace Attorney](https://en.wikipedia.org/wiki/Ace_Attorney) games. In each Ace Attorney game you play as a lawyer who has to "solve the case", they seem to be a bit adventure and a bit puzzle solving with very low legal realism. In some ways it's an inversion of a detective story, the game is usually won once you present evidence that you've uncovered that proves your client's innocence. From Wikipedia:

>The story follows Phoenix Wright, a rookie defense attorney who attempts to have his clients declared "not guilty".

There have been 11 official versions of this game but on this website they've made way more, using all the assets from the official games to make their own, and sometimes make their own assets. Well I should say, they are doing that on the real version of the website, on port 80. 8080 is a little sparse, I think they just use it to test the formatting of the page without any of the user-generated content.
![](/images/100Days/Day49/empty.png)
![](/images/100Days/Day49/full.png)

On the top you see the developer page, on the bottom is the live page.
![](/images/100Days/Day49/forums.png)

There's also forums (both in french and in english) and of course, the games themselves.
![](/images/100Days/Day49/girl.png)
![](/images/100Days/Day49/wright.png)
![](/images/100Days/Day49/gavin.png)
![](/images/100Days/Day49/mia.png)

I played them a bunch. They're all over the map in terms of quality, some are just bizarre fanfictions, some try to be "real" games. I'm amazed by the dedication, many of them have multiple installments and their own mini franchises. Some of them say they were in development for _over seven years_! It seems like a really passionate community.
![](/images/100Days/Day49/reddit.png)
I found some stuff about it on Reddit. Seems like it's got a pretty big following among the Ace Attorney Fandom. The game assets are pretty simple so it makes sense that it'd be easy to remix like this.

Attorney Online, the other site mentioned, looks pretty interesting also. But that's for another time. See you tomorrow.
