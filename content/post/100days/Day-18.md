+++
title = "Shodan Stories Day 18: Defaced Server in Walnut, Hacking in a Nutshell, These Jokes Don't Write Themselves!"
date = 2019-01-21T23:35:30-08:00
draft = false
tags = []
categories = ["100 days"]
+++

In what I hope will become an infrequently regular feature I decided today to look for an already hacked server that had been defaced. I had found one in the process of defacement on my very first day, but the fully defaced ones are interesting largely because of the tags left by the hackers themselves. I'm a little nervous about drawing attention to myself by publishing hacker tags in plaintext (easily found via Google alerts) so I'll mostly be doing that via images. Maybe I'll figure out a better way around this problem.

## A Hacked Server on 198.13.117.201
Shodan has a blog post on looking for hacked servers and they recommended starting off with the easy route: searching for "hacked by", as many hackers leave tags on the servers they take over. I did so and went with one of the first results, this one in Walnut, California.
![](/images/100Days/Day18/hacked.png)
Looks like it got completely had. Shodan indicates that it had been running services off of ports 21, 25, 53, 80, 143, 443, 465, 993, 995, 2082, 2083, 2086, and 2087. I was wary of doing my own port scan or any pentesting because I didn't want to draw any attention to the IP address of my friend's apartment, so I just went with what Shodan gave me, which is usually a little short of what I can find myself but c'est la vie. Given those ports it looks as though it was a typical webpage and email server with cPanel as the hosting interface. I really wanted to know about where the hackers had found the exploit, but I didn't want to poke around too much. Maybe being overly cautious.

So who is this group?
![](/images/100Days/Day18/thunders.png)
Looks like they are defunct as of this moment, having called it quits back in November. I'm a little stunned that they are on Facebook, but I suppose just about everyone is so why not them. Their page was full of exploit logs and past hacked pages, none of which are still up as defaced pages. Which raised the question, why was this one still up? This group stopped a few months ago so this page must have been around for awhile defaced like this. Had no one noticed? There was no DNS record for it so maybe the website owner just shifted their url to a new server and left this one to rot. But why not cancel the hosting?  I tried to look for more clues. The html of their defacement page had a few easter eggs of just swearing at me for looking at their code but also had a hidden youtube video link, however it seems like that video no longer exists. The links that they put in their page all had data loggers via a restful API to monitor clickthroughs but I couldn't tell where it was pointing toward. I think it might be a no go, I couldn't find any info on what this used to be, not in DNS and not in WhoIS. Possibly I could go onto their exploit list and check all the links to see which one this one goes to, but there are just too many links for that, they were very busy.

It looks like this group was fairly prolific and successful run between July 2017 and November 2018, and was even able to hack into [Costa Rican government websites](https://latesthackingnews.com/2018/05/16/costa-rica-government-websites-hacked-by-pakistani-hackers/) and some [IRS webservices](https://www.financialexpress.com/india-news/pakistani-group-hacks-i-t-dept-website-for-irs-officers/606398/). Their motivation seems to be both to sow general chaos and to strike out against those that they see as against Pakistani interests and values.

Yeesh, black hats give me the heebie jeebies. If this website goes down you'll know why. See you tomorrow.
