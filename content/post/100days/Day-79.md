+++
title = "Shodan Stories Day 79: Controlling the Climate in Constanta, Legacy Browser Extensions, Windows Virtual Machines, Reliable Old Internet Explorer, and Java Applet Deep Hell"
date = 2019-03-25T22:10:13-04:00
draft = false
tags = []
categories = ["100 days"]
+++

Real tough one today. I found a search for [Siemen's Saphir HVAC control systems](https://www.downloads.siemens.com/download-center/d/SAPHIR-ACX32-Hardware-Description_29538_hq-en.pdf?mandator=ic_bt&segment=HQ&fct=downloadasset&pos=download&id1=29538), and four hours later I was installing a Windows virtual machine.

## HVAC SCADA System on 5.2.229.60
The search itself was for "wince Content-Length: 12581". Many of the results on Shodan were in Romania, and so I picked one in Romania. It was running a webserver on 80.
![](/images/100Days/Day79/firstlook.png)
This is a pretty cool design for a SCADA opening page. It looks a bit like a crossword. Only the Open RMS and Open Treeview links were active.
![](/images/100Days/Day79/rms.png)
The remote monitoring system gave me a lot of access.
![](/images/100Days/Day79/config.png)
I could change the password, change what access rights were for different users, upload my own files, upload my own programs, set up my own monitoring.
![](/images/100Days/Day79/processes.png)
![](/images/100Days/Day79/files.png)
That's all well and good. I decided to check out treeview, and that's where the trouble began.
![](/images/100Days/Day79/treeview.png)
Lots of tantalizing things to click on. I really wanted to see those statistics. But whatever I clicked on I got the following error.
![](/images/100Days/Day79/java.png)
Now, most modern browsers have gotten rid of java [many years ago](https://jaxenter.com/clock-ticking-java-browser-plugin-will-deprecated-soon-131546.html), the one exception being good old Internet Explorer. Naturally IE only runs on Windows, and I'm sure you get where this is going at this point. Before I tried installing Windows, however, I tried several other more sensible options.


1. I tried this weird thing that Microsoft lets you do where you [Remote Desktop to access Internet Explorer 11 from Windows but atop OS X](http://osxdaily.com/2015/10/19/use-internet-explorer-11-mac-os-x-easy/#comments). I stopped because I didn't want to have to make a Microsoft account.

2. I installed Java 8 Developer Kit (very outdated) so that I could get a program called [appletviewer](https://superuser.com/questions/1394999/how-do-i-run-java-applets) that would allow me to download Java applets meant for a browser from their source and run them in their own Java runtime. Unfortunately even though I could download and run the applet, it was requesting data which my local applet didn't know how to find, so it didn't display anything.

3. I installed a four year old version of Firefox that allowed java plugins. It nearly worked.
![](/images/100Days/Day79/java2.png)
However, it gave me an error because my Java security settings were too high to run applets from an unknown source. It said I could whitelist the source or change my security settings in the Java Control Panel. Where is the Java Control Panel? It hasn't existed in the last 3 versions of OSX. I then tried to change the security settings via editing Java's own configuration files, but couldn't find where it was setting them.

4. I tried installing an old version of Firefox on my Kali Linux VM. I couldn't remember the right `tar` flags I needed to install it, and didn't have the confidence that I wouldn't encounter the same problem as I had on OSX, so I didn't end up trying too hard.

5. I downloaded a Windows VM. The download took two hours, and by the time it was done the host wasn't up anymore. I don't know why it would have gone down considering that it was the control system for what I assume was a building's HVAC, but now we'll never know.

Lesson learned: always have Windows already installed. See you tomorrow.
