+++
title = "Shodan Stories Day 61: Printing Skulls in Springfield, Tautulli Plex, and OctoPrint"
date = 2019-03-05T14:00:02-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today's episode is again taken off of the recent searches. I saw someone searching for "octoprint -login -authenticate", and decided I'd take a look. Turns out [OctoPrint](https://octoprint.org/) is a web interface for 3D printers that let you remotely monitor and control your in progress jobs.
![](/images/100Days/Day61/octoprint.png)
So I'd be finding 3D printers, a whole dimension up from the paper printer I found back on day 31.

## A Wanhao Duplicator i3 3D Printer on 173.17.200.211
I just went with the first result, in Springfield, Missouri. It was running on something on 3 ports, 8181, 9001, and 9002. 9002 was a [Plex media server](https://www.plex.tv/) login, which you may remember from days 9, 19, and a couple of others. 8181 was a login for [Tautulli](https://tautulli.com/), which I learned is a web application to monitor your Plex server's performance.

9001 had good stuff though, a webserver running the OctoPrint web interface.

![](/images/100Days/Day61/firstlook.png)
And it had a webcam attached so that you could remotely monitor your jobs!
![](/images/100Days/Day61/webcam.png)
Given what I see here I think it's a Wanhao Duplicator i3, since that printer also has a open off white bed.
![](/images/100Days/Day61/wanhao.png)
I don't have a whole lot of control over the printer with this panel, but I do have a whole lot of information.
![](/images/100Days/Day61/history.png)
I can see that the last print was all the way back in August, to print skull.gcode, and that there were over a thousand prints that happened before that. Why haven't there been any new ones in the past several months? It's hard to believe that these dates could be wrong. My theory right now is that this printer was sold and the new owner just now set it up. Seems a bit weird though, not sure if that is a good theory.
![](/images/100Days/Day61/success.png)
I can also see the past print data. Looks like whoever was printing here had more success than I have had 3D printing.

I could also download the last print job, which if you remember, was named _skull.gcode_. It comes as a format called [gcode](https://en.wikipedia.org/wiki/G-code), which is a language used to send controls to automated machine tools. It looks a bit like [assembly](https://en.wikipedia.org/wiki/Assembly_language), albeit much more human-readable. Take a guess what this sample of code is doing:

```
G1 X79.492 Y109.773 E0.85725
G1 X79.329 Y109.857 E0.86285
G1 X78.641 Y110.657 E0.89504
M106 S255
G1 X78.593 Y110.714 E0.89895
G1 X78.208 Y110.343 E0.92686
G1 X78.064 Y110.102 E0.94153
M106 S193.8
G1 X78.050 Y109.983 E0.94518
G1 X78.194 Y108.143 E1.00153
G1 X78.490 Y106.693 E1.04670
G1 X79.093 Y104.222 E1.12433
G1 X79.197 Y103.774 E1.13835
G1 X79.213 Y103.621 E1.14304
G1 X79.639 Y102.607 E1.17663
G1 X80.104 Y102.234 E1.19484
G1 X80.183 Y102.242 E1.19726
G1 X80.543 Y102.362 E1.20885
```
That's right moving the extruder nozzle through the x-y plane while printing the object. I think the parts beginning with E changes the extruder nozzle diameter. It's excruciating stuff, and skull.gcode had almost a million lines of it. I wanted to see what it looked like, and while you can convert gcode to more commonly seen 3D object files pretty easily and then open it in your 3D software of choice, I didn't have the time for that. Instead I used [an online gcode analyzer](http://gcode.ws/) to visualize it.

And here it is!
![](/images/100Days/Day61/skull.png)

It's a skull. I don't know what I was expecting. See you tomorrow.
