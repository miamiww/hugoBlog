+++
title = "Shodan Stories Day 67: Taking Care of Feet in Buenos Aires, Good Old Apache Webservers, and the Forgotten History of the Directory Index"
date = 2019-03-11T22:41:52-04:00
draft = false
tags = []
categories = ["100 days"]
+++

I saw a great search on Shodan the other day, one just for [Apache Webservers](https://en.wikipedia.org/wiki/Apache_HTTP_Server). Apache is a true classic, a webserver now 24 years old that had a big hand in the expansion of the early web. It's still among the most popular servers today; it's estimated that 20% of all current websites are running Apache.
[![](https://news.netcraft.com/wp-content/uploads/2018/12/wpid-wss-share.png)](https://news.netcraft.com/archives/2019/01/24/january-2019-web-server-survey.html)
So I was expecting to see a lot of results, and indeed Shodan could identify at least 320,000 IP addresses running Apache.
## An Apache Server on 181.229.222.94
With so much to go on, I decided to pick just the first result I found, in Argentina.
![](/images/100Days/Day67/firstlook.png)
A classic page. The ol' "Index of /" directory list. I remember seeing one of these for the first time maybe 20 years ago. I spent a good portion of the day trying to find any kind of scholarship, history, or journalism about this kind of directory page, but I couldn't find anything. If you know of anything like this please send it my way.

The little folders are directories and the "?"s are files. M leads to an empty array, and PU leads to an access page.
![](/images/100Days/Day67/access.png)
I downloaded one of the PU rar files and found that it had an entire PHP server and web page inside of it. When I tried to host it locally however, I found that it was full of errors and couldn't actually run. Maybe someone was scrambling to finish a web development job and never got it together. I didn't know enough PHP (or wanted to take the time to know) to figure out how to read the pages that I did have, but it included all of the images that the server was hosting, including this one.
![](/images/100Days/Day67/Fondo8.jpg)
I couldn't really figure out what was going on here, and I had more important things to look at anyway. TsT I couldn't get into but VA and VAweb are just great.
![](/images/100Days/Day67/VA.png)
VA opened up this truly amazing website for a podiatrist in Buenos Aires. Look at all those colors of text. I can't read a single word of the pink text. That logo is just beautiful. Unfortunately it seems like they aren't actually using this website, because I looked them up on Google and found that their [website looks like this](http://www.viviana-arias.com/):
![](/images/100Days/Day67/VAReal.png)
Amazingly that's also what the VAweb directory opens, which leads me to a theory that this index is the development area for a web designer to stage and showcase websites. By the way, if you didn't go to the page and see it in real life immediately, those images are an embedded flash animation.
![](/images/100Days/Day67/maps2.png)
Here it is in Google maps. The plant is the same, but it just doesn't look right without all the text scrawled in front of it. See you tomorrow.
