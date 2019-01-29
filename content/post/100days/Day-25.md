+++
title = "Shodan Stories Day 25: Helping Strangers in Singapore"
date = 2019-01-28T16:34:22-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I saw someone searching for "SingTel", and had given a description of the search saying "what? no auth? W o a h". Pretty compelling stuff, so I gave it a search myself. The actual query was a little more complicated, "Server: Arcadyan httpd 1.0 200 OK org:"Singtel Fibre Broadband" ".

## An Unsecured Router on 219.74.62.124

Every result for the search was in Singapore, which I realized is because [Singtel is one of the largest ISPs and mobile network providers in Singapore.](https://en.wikipedia.org/wiki/Singtel) I figured out that the search was for routers that had been provided by Singtel to its customers, probably for some kind of monthly fee and a huge installation cost (important PSA: never use the ISPs router! buy your own!). Shockingly the default on the routers seemed to be to have no password and to have the router configuration page accessible via the static IP address.
![](/images/100Days/Day25/therouter.png)

Meaning that I could... see the WiFi network name and password, see what devices were connected to the network, set up port forwarding, turn their computer into a botnet, spy on all of their traffic, etc. Least interestingly I could find out that their router model was a ["Singtel WiFi Gigabit Router AC Plus"](https://www.singtel.com/personal/support/broadband/routers-ont/arcadyan-ac-plus-guide). Now I didn't want to do any of that, so I decided to do something nice instead. I saw that their router uptime was only a little over an hour, and I realized that nobody else had likely gotten here before me, but that once they started arriving things would go bad for whoever owned this. So I set a password on the device.
![](/images/100Days/Day25/password.png)
I checked what the WiFi password was and set it to that, thinking that that would likely be their first guess if prompted with a password request that they were not expecting. Most people never check this configuration page after setting up their router anyway, and this way hopefully they never will have to.

I couldn't entirely help myself from poking around though, and I found that this router showed what other WiFi networks were in the vicinity so that you could pick the best channel on which to run your own network. Now the WiFi network they had was a fairly bland default, but I did notice a couple of networks that weren't so bland.
![](/images/100Days/Day25/signals.png)
I decided to check for amknet and LaiFamily in [WiGLE](https://wigle.net/), and found that there was just one lat-longitude combination that had both of those networks in Singapore.
![](/images/100Days/Day25/thehome.png)
And here it is via Google Maps. The router's in one of those buildings.

Looks nice. They're right by a country club. See you tomorrow.
