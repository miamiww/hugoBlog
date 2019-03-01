+++
title = "Shodan Stories Day 56: Buying Souvenirs in Bethlehem, Schneider Electric spaceLYnk, EXIF Data, and Does It Count as a Pilgrimage If You Are Just Remotely Opening and Closing Gates via a Store's Insecure SCADA System?"
date = 2019-02-28T12:01:30-05:00
draft = false
tags = []
categories = ["100 days"]
+++

I saw a search today for someone looking for [spaceLYnk logic controllers](https://www.schneider-electric.com/en/product/LSS100200/spacelynk-logic-controller/?range=62958-spacelynk&node=2640385230-products), a kind of logic controller for SCADA systems made by [Schneider Electric](https://www.schneider-electric.com/ww/en/) (SCADA, if you remember from day 30, stands for supervisory control and data acquisition).

![](/images/100Days/Day56/spaceLYnk.png)

## spaceLYnk SCADA System on 213.6.102.238
There were quite a few results from all over the place, but I noticed that most of them didn't have visualizations of the system. So I picked one that had the whole system mapped out, in Palestine.
![](/images/100Days/Day56/firstlook.png)
It's the control system for a building housing a store called Bethlehem Nativity Souvenirs, and, unsurprisingly at this point, I seem to have complete control over the system. I can turn lights on and off, open and close the gate, turn central fan systems on and off.
![](/images/100Days/Day56/cash.png)

I'm not doing any of that of course.
![](/images/100Days/Day56/outside.png)
![](/images/100Days/Day56/entrance.png)

These aren't live camera feeds by the way, they are just image stills. Images taken with a Nikon D7200 Camera on May 8th 2018 between 3PM and 4PM, using a AF-S DX VR Zoom-Nikkor 18-200mm lens. The serial number of the lens is 9418427. Yes I checked the [EXIF data](https://photographylife.com/what-is-exif-data), but I was desperate. For you see, even though I know the name of this store, even though I can turn its lights on and off and cause all other kinds of mayhem, I can't figure out exactly where it is.
[![](/images/100Days/Day56/bethlehemnativity.png)](http://www.bethlehemnativitygroup.com/)
They have a [website](http://www.bethlehemnativitygroup.com/).
![](/images/100Days/Day56/facebook.png)
And they have a Facebook page.

And on that Facebook page they have an address, but on Google maps, at that address, there is, well, see for yourself.
![](/images/100Days/Day56/oldshop.png)
Yes it is a Bethlehem Nativity Souvenirs store! But it is not the one in the SCADA visualizer, which is clearly a much more recent construction. Nowhere in any of their online presence do they indicate having another shop. The Google street view images are from 2017, so I thought that perhaps they remodeled, but I checked on Trip Advisor reviews of the hotel next door, looked through all of the recent images of the hotel to see if I could spot the store, and yes, as of late 2018 it appears that the store looks the same as it does here.

I also want to point out that this amazing, unique and original cafe is across the street.
![](/images/100Days/Day56/stars.png)
I fruitlessly searched Google maps for a bit, looking either for it a place that could inhabit this newly renovated building. The closest I got was this building.
![](/images/100Days/Day56/oldversion.png)
If you look at it just right, then... maybe? No, it's pointless. I should just call them.

But speaking to another human? That might be a step too far. Plus, how to explain? See you tomorrow.
