+++
title = "Shodan Stories Day 30: Automating Buildings in Copenhagen, the BAS SCADA Industry, Expandable Controllers, Cloriūs, KeRo, and O&J CTS A/S"
date = 2019-02-02T22:37:32-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I decided to go looking for [SCADA systems](https://en.wikipedia.org/wiki/SCADA). SCADA stands for supervisory control and data acquisition and is a type of widely used industry management software, typically made bespoke for a particular factory or building. For a little more information I'll let the man himself, Carl Gould, take it away.
{{< vimeo 127089533 >}}

## SCADA Building Automation System on 80.71.129.61
Not really sure how to find one, I just searched on Shodan for "SCADA" hoping to reap rewards with little research. I was not disappointed, as it seems that many SCADA systems declare themselves as such. Quite a few results prompted immediate logins or no-auths, but I found one in Denmark that had a landing page before the login with enough information to start digging.
![](/images/100Days/Day30/system.png)
The text on the page discusses how to get the extremely high customer service and repair services from a company called O&J CTS. There are two methods to login to the actual SCADA interface, via Java and via HTML5. Based on what I've gathered on SCADA it seems like quite a bit of the market is still Java applets working via the browser, which might explain why some analysts are [predicting the oncoming end of the SCADA industry](https://controltrends.org/controltrends-news/news-and-information/11/are-bas-and-scada-systems-doomed-is-blue-pillars-digital-energy-network-next/).

Trying to login via HTML5 yields the following login with an HTML5 canvas underneath currently only showing the logo for BA Systems. I bet that if I successfully logged in the canvas would populate with lots of cool diagrams showing pipe flow and conveyor belt speed, all updating in real time.
![](/images/100Days/Day30/login.png)
So what is this system automating exactly? Here we have to split into several directions.

### O&J CTS A/S
The landing page talks about how O&J CTS (A/S is like the Danish "GmbH" or "LLC") is the one to call to perform any maintenance, and also includes [a link to their website](http://www.oj-cts.dk).
![](/images/100Days/Day30/cts.png)
In Google translate's words "CTS is short for Central Condition Control and Control. A CTS System is an intelligent energy and climate control system that balances comfort, consumption and operation in larger buildings". The company seems to install and manage these systems. So perhaps this is an energy management and climate control system for a large office building, maybe even one of the ones listed on their [client references page](http://www.oj-cts.dk/referencer)?

### KeRo Systems and BA Systems
Two other names stand out however. On the same landing page there is a link to a copyright page, which declares that the copyright for the software belongs to [KeRo Systems](http://www.kero.dk/).
![](/images/100Days/Day30/KeRo.png)
Reading the last couple of lines on the image up above there, I can see that they used to have a software product line called ISC Series that had been rebranded to [BA Systems](http://www.basystems.dk/forside). Which should sound familiar to you.
![](/images/100Days/Day30/basystems2.png)
BA Systems makes sensors, components, and software, so it seems likely that O&J CTS A/S either subcontracted out the development of the software to them or had purchased a product off the shelf.

### Cloriūs Controls A/S
However I was a bit thrown for a loop when I checked out the manual for the system (linked to in the landing page), which had the logo for a company named Cloriūs all over it and had a bizarrely similar image of the landing page as its example but without the O&J references replaced by Cloriūs.
![](/images/100Days/Day30/bizz.png)
That's even the same tiny pixelated image of two men working on a pipe.

Clearly some kind of corporate skullduggery had occurred here, but just what exactly? At first I thought that perhaps Cloriūs had been bought out but no one had bothered to change the manuals, but no, Cloriūs remains in the land of extant corporations.
![](/images/100Days/Day30/clorius2.png)
They even have a reasonably diversified product line. But I couldn't find any reference to an "ISC SCADA" product or even any kind of SCADA product on their website. On Google though I did find an [alert from the US Department of Homeland Security's Industrial Control Systems Cyber Emergency Response Team](https://ics-cert.us-cert.gov/advisories/ICSA-15-013-02) that Cloriūs ISC SCADA systems had a major security flaw in their Java web client, as well as the [manual for another type of Cloriūs control system](http://www.cloriuscontrols.cn/pdf/GB/5005-GB.pdf).

Getting deep deep in the weeds of Danish industry press releases I was able to suss out that O&J CTS had purchased Cloriūs's entire building management system department on December 1, 2017.

AHA. CASE CLOSED. So O&J CTS did purchase a (part) of Cloriūs, and then had never bothered to update the manual for their new systems with the new corporate branding. In addition they changed precious little on the system landing page other than their own logo. Either O&J purchased components or subcontracted out work to BA Systems (formerly KeRo) or Cloriūs previously had in the development of their system.


So uh what does the system do again? See you tomorrow.
