+++
title = "Shodan Stories Day 31: Youth Volunteering in Guri, ePrinting, Jetdirect, Requiem for a Hewlett Packard, the State of Civil Society, and Hand Massages for the Elderly"
date = 2019-02-03T21:23:52-05:00
draft = false
tags = []
categories = ["100 days"]
+++

I saw a search on Shodan for "Jetdirect" with the tagline "unsecured printers". I'd recently heard a story about fans of the [Youtuber PewDiePie using Shodan to hack into 50,000 printers to print messages about him](https://www.theverge.com/2018/11/30/18119576/pewdiepie-printer-hack-t-series-youtube) so I thought maybe I could take a look and see maybe how they had done it.

## HP Officejet Pro 8100 N811a on 121.161.211.66
Shodan showed 18,000 results for Jetdirect, with a plurality of them being in Korea. It seems like the printers recieve print jobs via port 515, but I found hat many of them were running webservers on port 80. I picked one of the ones with a webserver so that I could have more to go on.
![](/images/100Days/Day31/firstlook.png)
Now there is quite a bit of information here. I see immediately the model, and then the ink levels.
![](/images/100Days/Day31/printerbuy.png)
Checking out this model on Hewlett Packard's website I found that it did match up with the imate shown in the web app. Unfortunately this model is now discontinued however :( Let's take a moment of silent reflection for all of the enterprise level hardware that's been discontinued and is no longer supported but still being used with unupdated firmware.


...

From here I quickly got that same feeling of vertigo from over-connection that has become such a frequent part of my day to day life. I found that I could:

* set the password
* print anything I wanted
* order more ink
* hit "agree" on new user agreements
* change the time on the device
* enable streaming of logs via UDP
* sign myself up for email alerts whenever the printer was low on ink
* scan their own network for other devices

and way more than that. I had total control over this printer. I could brick it, make it print out obscure memes about my own favorite Youtubers (anyone who posts [Kids In The Hall Clips](https://www.youtube.com/watch?v=91ahZDmqEQQ)), set up surveillance on it and all the other devices on the network until the end of time. What I could not do directly though is figure out who owned the printer. I could see how much they printed however!
![](/images/100Days/Day31/usage.png)
23639 pages, that's a lot of paper! And only one paper jam! Since the printer had only been on for this particular data session since August 2018, I had to assume that this was a corporate machine. I did have a significant clue in the wifi network name.
![](/images/100Days/Day31/network.png)
Having successfully using [WiGLE](https://wigle.net/) I thought that I would be able to find out where this printer was based on the network name, but unfortunately "guri1365" wasn't in their database.

About to give up, and with very little hope, I decided just to Google the network name. Shockingly, there was a webpage named guri1365.or.kr, a Facebook page named guri1365. Moreover, there was an entire organization named [1365](https://www.1365.go.kr), of which guri1365 was the Guri City branch.
![](/images/100Days/Day31/volunteer.png)
1365 is a volunteer coordination organization that has branches all across Korea. They seem to be open toward all kinds of volunteers, from families to high school students to corporate teambuilding groups, and both connects volunteers to outside organizations that need volunteer staffing and runs community and civil society events of its own. Their tagline is "Making a world that lives together in the spirit of service and sharing".
![](/images/100Days/Day31/guri1365.png)

The Guri branch seems to have a wide range of programming, with quite a few events for youth volunteers.
![](/images/100Days/Day31/gallery2.png)
Some recent activities included cooking for the homeless, fundraising for migrant children, helping out at a nursing home, and making crafts for the elderly. The most recent activity, from just a couple of days ago, was a huge event for giving hand massages for the elderly.
![](/images/100Days/Day31/handmassage.png)
From the looks of their documentation of the event about three dozen teenagers volunteered to give the hand massages, which were open to old people to come get a free hand massage.

Based on information on their website it seems like the headquarters for the Guri branch are in the Guri Youth Center, where they stage most of their events. Lets take a look at it via Google maps.
![](/images/100Days/Day31/youthcenter.png)
I didn't see any confirmation from the signs on the front of it that 1365 had residence inside, but the Google maps imaging from Guri dates to 2015, so it's hard to make any definite statements.

It seems really nice. I can't imagine teenagers in America volunteering to give hand massages to the elderly, not because teens here are bad or uncaring, but because that kind of restorative physical touch is almost taboo here. What is the state of America's touch-culture? Please send me any scholarship you might have on this topic. See you tomorrow.
