+++
title = "Shodan Stories Day 80: Managing Apartment Security in Bangkok, IoT Defacements, and My Wifi Video Door Lock Makes Me More Safe Because It Lets Anyone Remotely Monitor My Home For Intruders"
date = 2019-03-27T11:26:26-04:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I saw a search for "comelit multi apartment gateway". Sounded pretty interesting so I jumped in. The query was "input_box==true window.open reboot.html"

## Apartment Door Lock Management System on 184.82.206.184
[Comelit](https://www.comelitgroup.com/en-us/) is a manufacturer of IoT video doorbells and locks. This search seemed to be showing up the configuation pages for apartment owners and supers, who assumedly had either retrofited all of the apartments in their building to have these wifi locks or had built a new building with them. This is a system meant for the apartment overseer, not the apartment dwellers. There were about 70 results and I picked one in Thailand.
![](/images/100Days/Day80/password.png)

On the apartments tab I could look at all of the apartments, and could see from the description that I wasn't the first person here. Toxic Mask had been here before.
![](/images/100Days/Day80/firstlook.png)
We can talk about TM in a second, first just look at how much access this system gives me.
![](/images/100Days/Day80/codes.png)
I can see the room numbers and _door unlock codes_ for every apartment in the building. I can make changes to those codes, _locking people out of their apartments_. I could do that for every apartment, change the password on this configuration system, and cause mayhem for ~100 people likely for hours. What is the benefit of having your doors connected to the internet?

I found TM on [defacer.id](https://defacer.id), the website that ranks web site vandals based on their defacements. [His page on the site](https://defacer.id/archive/attacker/toxic-mask) indicates they've vandalized 1249 websites since starting in 2017.
![](/images/100Days/Day80/toxicmask.png)
This is their vandal tag. Looks way more impressive than the one one the lock gateway, but I guess that IoT configuration pages don't give you too much to work off of. See you tomorrow.
