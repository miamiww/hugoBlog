+++
title = "Shodan Stories Day 48: Processing Wood Products in Piet Retief, Dahua Botnets, MikroTik Botnets, and Particle Board"
date = 2019-02-20T15:47:18-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Kind of a weird one today. I didn't like any of the searches I'd seen so I decided to search for anything that had "production plant" in the title.

## A Woodchem Production Plant on 154.126.209.18
I wasn't entirely sure what I was looking for, but got several dozen results. I decided to pick one in South Africa.
![](/images/100Days/Day48/firstlook.png)
On port 80 it was running a login for a [Dahua](https://www.dahuasecurity.com/) Technology device. Dahua mostly makes surveillance products like cameras and patrol drones(!) but in researching them I also found that their products are infamous for [being used for botnets](https://www.hackread.com/bashlite-malware-linux-iot-ddos-botnet/).

There was also a service running on port 1723, I couldn't tell exactly what it was but in the banner it said:
```
Firmware: 1
Hostname: Woodchem-production-plant-CRS
Vendor: MikroTik
```
[MikroTik](https://mikrotik.com/) is a manufacturer of routers and other network devices that is [also well known](https://www.trendmicro.com/vinfo/us/security/news/cybercrime-and-digital-threats/over-200-000-mikrotik-routers-compromised-in-cryptojacking-campaign) for [getting hacked](https://www.zdnet.com/article/thousands-of-mikrotik-routers-are-snooping-on-user-traffic/). So not the best sourcing from this possible woodchem production factory.
Woodchem by the way both seems to be [a conference](http://www.woodchem.fr/en/) about the wood products industry and a [company that has invested in South Africa](https://www.kap.co.za/portfolio-posts/producing-at-higher-volumes/). After reading a few different press releases I think this factory that I found is likely in Piet Retief, run by a company called [Safripol](http://www.safripol.com/), which is a subsidiary of KAP Industrial Holdings Limited, a large industrial multinational.
![](/images/100Days/Day48/safripol.png)
There were several wood related factories in Piet Retief, as its main industry is timber, but I was able to figure out that it's probably this one, as seen from Google maps.
![](/images/100Days/Day48/factory.png)
Their main output is urea-formaldehyde resin, which is then used in the manufacture of processed woods like particle boards.

I wonder where those particle boards go? See you tomorrow.
