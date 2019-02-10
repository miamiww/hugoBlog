+++
title = "Shodan Stories Day 38: A Clothing Store in Moscow"
date = 2019-02-10T12:11:44-05:00
draft = false
tags = []
categories = ["100 days"]
+++

A quick cam day today because I'm a busy bee. I found a search awhile back for "Auther: Steven Wu". Yes with the typo. It seems that Steven Wu wrote some server software for networked cameras back in maybe 2009 that is now used in a few different camera brands, all of which allow for snapshots to be taken without a password even if the video feed itself requires a password.

## TRENDnet Camera on 195.68.183.190
Most of the cameras that this search turns up are in Japan and most seemed to be in parking lots. Since there were a couple of thousand results, all of which were accessible, there was a fair amount of variety. I picked one in Moscow that appeared to be of a clothing store, complete with a few shoppers. This one was manufactured by a company called [TRENDnet]([TRENDnet](https://en.wikipedia.org/wiki/TRENDnet)).
![](/images/100Days/Day38/bloke.png)
I was able to see a single still image from the camera that updated each time I reloaded the website. The rest of the features required a password. Interesting design choice. Occasionally when I reloaded the image would be completely glitched out.

Tantalizingly, the name of the store seems to be on that back wall, but I couldn't make it out. That's probably for the best. See you tomorrow.
