+++
title = "Shodan Stories Day 27: A Connoisseur of Sorts in Shenzen, Western Digital 2 Go, and Rest In Peace TwonkyMedia"
date = 2019-01-30T00:04:46-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Saw somebody doing a search for "twonky". What a name! I had to find out about it.

## A Twonky Media Server on 14.155.113.144
[Twonky is one of many personal media servers](http://www.lynxtechnology.com/twonky-overview) I've now run into, meant to run either [on a network attached storage device or on a computer.](https://twonky.com/index.html) The purpose I assume is to be able to stream your media from any devices on your network without having to worry about storying them locally (so if you've stolen a lot of blueray movie rips from bittorent and want to watch them on your phone or something). It looks like Twonky has had a [fairly rambunctious ownership history](https://en.wikipedia.org/wiki/TwonkyMedia_server), and was formerly known as TwonkyMedia, and then split off as just Twonky but TwonkyMedia existed under German ownership as a competitor to Townky until the German company went under and TwonkyMedia became unsupported. Goodbye TwonkyMedia, may you go off into the long dark night of unsupported but likely still used niche consumer grade software.

Anyway I picked the first IP I saw that had a real result, this one in Shenzen China. Generally Twonky seems to be meant for local networks only so I had to wade through a quite a few dead ends, but some enterprising users set up port forwarding so that the whole internet could see. Twonky seemingly tends to run a webapp on port 9000 as a default, so I visited that port in my browser.
![](/images/100Days/Day27/twonky.png)
Interesting song to photo/movie ratio there. Must not be much into music. I wonder what they are into?
![](/images/100Days/Day27/bangin.png)
Hmmm.

![](/images/100Days/Day27/wankit.png)
I see.
![](/images/100Days/Day27/hornydoc.png)
<font size="50">🧐</font>
![](/images/100Days/Day27/pissing.png)
<font size="50">🧐🧐🧐</font>

They also have some like regular movies making for some truly delightful juxtapositions.
![](/images/100Days/Day27/readyplayerone.png)

So it's like 95% porn. Someone put their porn stash out there for all the world to see without realizing at all what they were doing. It kind of sucks to be honest, because what little content isn't porn or blueray movie rips seems to be personal photos and videos. This is running on some kind of network attached storage device (okay so I figured out the device - it's a [Western Digital 2 Go device in the My Cloud Home line, the ssl certificate gave it away](https://support.wdc.com/knowledgebase/answer.aspx?h=p1&ID=19493&lang=en&p=207) that this server software has wider access to than just the media files being hosted.
![](/images/100Days/Day27/filesystem.png)
You have access here to the entire file system of the device. The part I blocked out was the person's name, which they are using as their home folder.

So you can download any file on the device, explore the file system, upload your own files.

[Hachi machi](https://www.youtube.com/watch?v=O4foeo3oY-E). See you tomorrow.
