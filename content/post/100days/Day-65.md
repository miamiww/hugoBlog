+++
title = "Shodan Stories Day 65: My Wifi Enabled Smart Projector Helped Me Rekindle My Marriage's Lost Spark in Beijing"
date = 2019-03-09T23:45:45-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I wanted to find any kind of Alexa-compatible device, be it WiFi plug, smart bulb, or whatever, so I searched in Shodan for "alexa". After looking at the results for awhile I found that there was a particular type of object that showed up that I thought was worth looking into further, what looked like a "smart projector".

## Optoma on 54.223.86.54
The actual search I used to narrow down on the projectors was "alxtest/alexa", which was part of the name in the webserver these projectors were running. There were only 8, and I picked one in Beijing. It was only running webservers, the typical 80/443 pair.
![](/images/100Days/Day65/firstlook.png)
I obviously couldn't get any farther past this point, but I did experience one other thing on this page.
![](/images/100Days/Day65/cookies.png)
A cookies warning banner! Since when have these types of device logins involved cookies. It's making me wonder if maybe this is actually running off of Optoma's servers, and you can control your device via their server, which sends out commands to your projector. Seems crazy, but who knows anymore, Optoma might really need to put that tracker your browser.

So what kind of projector is this anyway? One that connects to the internet, clearly, and made by Optoma. It seems like Optoma is, at the moment, the only mainstream projector manufacturer making "smart" projectors, and they only have a few in their smart line. Narrowing it down further by publicity as a proxy for market share (one projector has [many more press releases by Optoma than the others](https://www.optoma.com/us/optoma-delivers-first-home-theater-projector-compatible-with-google-assistant-and-amazon-alexa/#)) this is likely an [Optoma UHD51A](https://www.optoma.com/us/product/uhd51a/)
![](/images/100Days/Day65/optoma.png)
This seems totally absurd to me. A voice enabled projector. Where's all the cords? Struggling with a VGA cable? A projector, by its complexity and its specificity, is an inherently anti-consumer product, and "home theater" marketed projectors tend to lack the quality or the functionality of "professional" models. It's got too many controls and too many features for a voice interface to really work out. Are you going to call out the kerning you want every time? Plus, this ad is just bonkers.
{{< youtube b_CU-wUEp1g >}}
What's the real angle here? To fill that niche market of smart home devotees with $1500 to spend on a new projector? To collect viewing metadata to feed into Optoma's growing stash of personality profiles?

Maybe they're just out there to save marriages and make "the game" a little more fun. See you tomorrow.
