+++
title = "Shodan Stories Day 89: Reading License Plates in Pretoria, Raspberry Pi Servers, and Storing Passwords in Plaintext"
date = 2019-04-09T00:22:39-04:00
draft = true
tags = []
categories = ["100 days"]
+++

Well I went looking for another nice pastoral IP camera scene but instead I found something pretty interesting: automatic license plate readers (ALPRs) in South Africa made by the ominously named company [Snipr](https://www.snipr.co.za/). These were a little different than the ones I found on day 10, which were enclosed systems . The ones I found today instead essentially are running off a Raspberry Pi and sending the the license plate images to Snipr's server, which then sent JSON back with the information about the license plate. These seem geared towards consumers rather than parking garage owners or police forces. I made a search to find them again, for "Snipr Configuration".
![](/images/100Days/Day89/snipr.png)

## ALPR Configuration Page on 192.143.90.182
I more or less chose a camera at random. They were all in South Africa, running webservers on some variation of the common 8080 or 8000 ports (like 8081 or 8181). The one I chose was running a webserver on 8081 and an ssh port on 2222. From the ssh info on Shodan I could see that it was running [Raspbian](https://www.raspbian.org/), so this was a Raspberry Pi. The webserver more or less confirmed this.
![](/images/100Days/Day89/firstlook.png)
Now what's interesting about this is not the authentication, but rather the "Setup" and "Debug" tabs.
On setup I can see all the ALPR cameras that are on this Pi's network... and change their passwords.
![](/images/100Days/Day89/setup.png)
On the debug tab I can see the logfiles, which include the locations of the images the cameras are taking, _all of the license plate numbers it reads_, and ___the username and password of all logins into the system___. All stored as plaintext.
![](/images/100Days/Day89/debug.png)
What a price we pay for keeping our neighborhoods safe from the wrong kinds of license plates. See you tomorrow.
