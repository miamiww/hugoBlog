+++
title = "Shodan Stories Day 32: Red Lion Industrial Controls in a Remote US Location, Riding the XetaWave, the AirLink ACEmanager, Tank Batteries, and the Stack Overflow Answer that Launched 6000 Redirects"
date = 2019-02-04T17:27:29-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I decided to go looking for for industrial control systems made by a company called [Red Lion Controls](https://www.redlion.net/). Red Lion makes controllers, touch screen operation panels, and a few other things besides. Reading Shodan I found that I could find them by searching for devices using port 789, which is the default port that Red Lion's software uses to communicate.

## A Red Lion Controller on 166.167.27.6
I just went with the first result, this one somewhere in the US on a Verizon wireless mobile network, and immediately got sucked into figuring out whatever was going on with it. Sure enough it was running Red Lion Controls on 789, but was also running webservers on ports 5000, 5001, 8080, 8081, and running an FTP server on 7001.

Before we really get into exploring what is in each of these webservers, I want to take a quick digression. I noticed from Shodan that the webservers on 5000 and 5001 give immediate redirects, and I wanted to see what the original redirect page looked like.
```
👻🌵🔮 $ curl http://166.167.27.6:5000/
<!DOCTYPE HTML>
<html lang="en-US">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="refresh" content=0";url=0Menu.htm">
    <script language="javascript">
        window.location.href = "0Menu.htm"
    </script>
    <title>Page Redirection</title>
</head>
<body>
<!-- Note: don't tell people to `click` the link, just tell them that it is a link -->
If you are not redirected automatically, follow the <a href='0Menu.htm'> link</a>
</body>
</html>
```
Notice the comment here. `Note: don't tell people to 'click' the link, just tell them that it is a link`. That seems like an oddly passive aggressive note for a boss to leave for the front end designer of an industrial products company. It seemed so strange that it stuck with me. Why leave the comment in at all when its direction had clearly already been followed? Who is the intended audience for this? I became... curious. And I wanted to see if the comment showed up in any other websites. So I did what any of us would do when they wanted to search within the source code of every web page in existence, I searched for the comment on [PublicWWW](https://publicwww.com/).
![](/images/100Days/Day32/publicwww.png)
What I found here astounded me. This exact comment, verbatim, is in six thousand web pages. Six thousand!! In a flash of insight I had my answer: the slightly arch tone, the widespread use. This code comes from someone's Stack Overflow answer. [And here it is](https://stackoverflow.com/questions/5411538/redirect-from-an-html-page/5411601#5411601).
![](/images/100Days/Day32/stackO.png)
This is the earliest use of the comment I can find, from 2011, although many people seem to use this html page as an example of the Platonic redirect, some with attribution to this answer. It's beautiful, isn't it? How much of the web is copy/paste. [Imagine if copy/paste had never been implemented as a widespread feature](https://en.wikipedia.org/wiki/Cut,_copy,_and_paste). [☃](https://www.copypastecharacter.com/) I'd have never been able to type that little snowman, that's for sure.

Well let's return to the webservers. What that 5000 port redirects you towards is a web server for a [XetaWave Ethernet Bridge](http://www.xetawave.com/).
![](/images/100Days/Day32/xetawave5000.png)
To be honest I'm not totally sure what the XetaWave products do. From their website they offer "A single, programmable radio that can meet diverse application needs simplifies and reduces the cost of implementation and ongoing management of a wireless communication network. The Xeta Series of radios are designed for applications across multiple industries including oil and gas, water and wastewater, electric power, industrial controls and the military." Reading the manual helped a little.
![](/images/100Days/Day32/manual.png)
Poking around didn't help that much but unsurprisingly at this point I had almost complete control over the device. I could send test messages, create a new password since there wasn't one to begin with, take it offline, change all of the ports, change all of the logging to send it to me, etc. Since I didn't want to do any of that I moved on to 5001.
![](/images/100Days/Day32/xetawave5001.png)
Another XetaWave! This one named "27 Chestnut East Middle" I thought that maybe that would be a clue to finding out what was going on with these things but no, there seem to be at least a dozen homes and apartment buildings with the address "27 Chestnut" and East Middle isn't much to go on. Unlike the first this one is sending signals to a fixed IP address run by Comcast Business, but I couldn't figure anything out about this IP. I could tell that it was up but it wasn't returning anything from scans except for the one destination port I already knew about. I dropped the lead and moved on.

![](/images/100Days/Day32/logsA.png)
On 8080 and 8081 are two Red Lion webservers, both very similar. The first, on 8080, has logs via [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) file for four tank batteries' levels over the past day.
![](/images/100Days/Day32/logsB.png)
[Tank batteries](https://www.petropedia.com/definition/3852/tank-battery) though! That's an exceptionally precise term for a device used to store crude oil immediately after it has been produced from a well. So these devices must be on an oilfield! Which would explain all of out-in-the-field-grade gear, and why this IP is on a mobile network.

On the remote view I could see what was on the Human-Machine Interface's (HMI) screen (that's the fancy name for a touch screen with some data on it that gets used in the industrial control industry - not sure when we stopped calling keyboards and mice human machine interfaces... what's the history there?)
![](/images/100Days/Day32/remoteView2.png)
This one uhh seemed to be broken. So I moved on.

The 8081 webserver _also_ had logs for four tank batteries, seemingly with different values from the first though so assumedly these are different tanks. Its HMI viewer seems to be working however.
![](/images/100Days/Day32/remoteView.png)
Hmm.
![](/images/100Days/Day32/airlink.png)
The final webserver is running this login page for a [Sierra Wireless](https://www.sierrawireless.com/) [AirLink ACEmanager](https://www.sierrawireless.com/resources/QtrlyNewsletters/Announcements/AceWare_Mar08_Announce/AceWare_Mar08_announce.html). Sierra Wireless makes a wide variety of "IoT connectivity and solutions" type devices but their [AirLink line](https://www.sierrawireless.com/products-and-solutions/routers-gateways/airlink/) is their branding for their "rugged, field-ready" cellular routers.

So this is the router connecting all of these little boxes, out in some oil field, out in the middle of America. And then connecting them all to me. See you tomorrow.
