+++
title = "Shodan Stories Day 35: Library Kiosks in Duchesne, Session Management Solutions, and True Friendship"
date = 2019-02-07T00:16:01-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Saw an amazing search on Shodan today: someone searched for "kiosk" with the comment "lotta cool stuff". Lotta cool stuff! How could I resist.

## A Library Kiosk Management System on 104.239.140.99
Most of the kiosks seemed to be library kiosks, I even found one from my alma mater's library! I ended up going with the first one that I couldn't immediately figure out the purpose of. It was running some kind of web server on port 3000.
![](/images/100Days/Day35/firstlook.png)
It seemed to be a scheduling application. It was running the same service on 3001 with different patron names.
![](/images/100Days/Day35/secondlook.png)
Rather than rack my brain for possibilities though I just Googled the service - [Libki Kiosk Management System](https://libki.org/).
![](/images/100Days/Day35/libki.png)
So Libki is a system for booking time on computers - more or less, meant for libraries and computer labs.

Now I knew that the system I was looking at was running on a cloud server, but I wanted to know where the actual computers that were being booked were. So I checked it with `host` to see if anything showed up.
```
👻🌵🔮 $ host 104.239.140.99
99.140.239.104.in-addr.arpa domain name pointer duchesne-libki.bywatersolutions.com.
```
Looks like the IP address is for the domain name duchesne-libki.bywatersolutions.com.
![](/images/100Days/Day35/bywatersolutions.png)

Looking at [ByWater Solutions's website](https://bywatersolutions.com/) I found that they were actually the makers of Libki, among other software solutions aimed at the library market. The owners seemed really sweet. Maybe I'm just feeling hormonal but when I checked their website's WhoIS record and saw that it had one of the owner's real name and personal email address on it I got kind of choked up. So innocent!
![](/images/100Days/Day35/theguys.png)
By why were they running their own session managing at their company? For testing? Or because they all share computers?

Looking a little harder at the url though, I had an insight: _duchesne_-libki. Duchesne, as we all know, is the name of a county in Utah. Counties typically have libraries in them. And in fact there is a Duchesne County Library in Duchesne county. And _in fact_ the Duchesne County Library uses Libki.
![](http://www.duchesne.utah.gov/wp-content/uploads/2017/01/Duchesne-Branch-crop.jpg)
How do I know that they use Libki? I checked the [Duchesne County Library Board Meeting Minutes of September 17, 2015](https://www.duchesne.utah.gov/wp-content/uploads/2017/01/2015-09-Duchesne-County-Library-Board-Meeting-Minutes.pdf), which clearly states the following:

_Libki – Patron computer management system is now functioning at both libraries to allow reservations for time
slots on the computers_

![](/images/100Days/Day35/meetingminutes.png)
Two libraries! That explains the two systems, on 3000 and 3001.

Thank you, public records, and thank you libraries, for championing public space in an age of its retraction from daily life. See you tomorrow.
