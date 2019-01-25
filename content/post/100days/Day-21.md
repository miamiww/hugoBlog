+++
title = "Shodan Stories Day 21: POWERful Plates in Fargo, Digital Signage, Unsecured Pis, and the Cold Cold Midwest Winter"
date = 2019-01-24T21:45:24-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I saw someone searching for "Screenly OSE" and actually gave a description for their search saying "screenly ose for the pi, think of a billboard system".  So I gave it a go.

## A Raspberry Pi Digital Sign on 140.186.23.181
[Screenly](https://www.screenly.io/) is a software for doing [digital signage](https://en.wikipedia.org/wiki/Digital_signage) off of a Raspberry Pi. They have a "Pro" version for quite a bit of money ($20/month minumum but up to $800/month) and [also an open source edition](https://www.screenly.io/ose/), which is what [OSE](https://github.com/Screenly/screenly-ose/wiki) stands for. Interesting to note that in Screenly's comparision between the free and the paid version, they mention that the open source version can do remote but not securely.

![](/images/100Days/Day21/prepper.png)
The first Screenly I found was displaying someone's nudes, which I did not want to publicize, so I instead picked one in Fargo, North Dakota. Yes I chose it because of the movie. It was only running one service, on port 9000, and I visited it in the browser.
![](/images/100Days/Day21/screenly.png)
The UI lets you add images and then cycle between images being displayed, but does not let you directly see what the images are that are being displayed. It also lets you see where on the pi the images are being stored - note this lets you see the username of the pi as well. In this case they have stuck with the default of "pi". This thing isn't that well secured so they probably have the default password as well 😈. Good thing I'm just a tourist or I could add it to a botnet.
![](/images/100Days/Day21/vertical.png)
However I did find that you could download a backup of the Screenly which lets you see all of the images being displayed, which is how I was able to figure out that this Screenly was being used to show a menu for a restaurant/meal service called Power Plate Meals. Or is it POWER Plate MEALS?
![](/images/100Days/Day21/powerplate.png)
[Power Plate Meals is a mini chain](https://www.powerplatemeals.com/) in North Dakota, with two locations in Fargo. It seems as though their business model is that they ship out meals (via UPS) as well as cater, though you can go to one of their brick and mortar location and get meals to go. Possibly they have tables where you can eat, but everything is pre-packaged.

The food looks... okay I guess. Not what I'd go for. But maybe in those cold cold North Dakota winters, with the snow coming down outside and the wind howling around your suburban neighborhood, maybe then you pull out a Power Plate Meatless Zucchini Lasagna out of the freezer and microwave it, drink a [glass of Fisheye Chardonnay](https://scontent.harristeeter.com/legacy/productimagesroot/DJ/8/693568.jpg) alongside as you eat it and it tastes just right, tastes like being safe in the storm and not having to go outside.

Yeah that would be perfect. See you tomorrow.
