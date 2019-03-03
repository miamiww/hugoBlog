+++
title = "Shodan Stories Day 58: Climbing the Global Cyber Vandalism Ladder in Westminster, Crypto Airdrops, and the Shady Underworld of Monetized Link Shortening Services"
date = 2019-03-02T22:09:27-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I felt like going for another hacked website, so I again searched for "hacked by" on Shodan like I did all the way back on day 18.

## A Hacked Server on 94.76.219.226
There were so many results, I picked the first one I got, in the UK. It had ftp and ssh running, as well as email and the usual 80 and 443 webservers. It also had a [cPanel](https://en.wikipedia.org/wiki/CPanel) login page running, cPanel being, in my experience, the most miserable way to run a webhost backend. But I'd come here for the webservers.

![](/images/100Days/Day58/firstlook.png)
What I immediately noticed was that they had embedded the most faux-epic threatening music I'd ever heard into the page. You can listen to it too without going to the page because it turns out they were looping the audio from this youtube video via an iframe: https://www.youtube.com/watch?&v=57A29qbGN-4
Again I don't want to type out any hacker names because I don't want to bother with them finding me because they had a Google alert set up.

Unfortunately both this hacker's linked Facebook page and personal website seem to be gone. There are three active and fairly interesting links.

### zone-h and defacer.id
![](/images/100Days/Day58/zoneh.png)

The two top left links that aren't Facebook go to the hacking collective's pages on zone-h and defacer.id respectively. [Zone-h](http://www.zone-h.org/) is [an archive for defaced website](https://en.wikipedia.org/wiki/Zone-H), started in 2002 seemingly largely as an appreciation for "digital graffiti" as an art form.
![](/images/100Days/Day58/defacer.png)

[defacer.id](https://defacer.id/) is much more of a "leaderboard", collecting all of different hacker collectives' stats and conquests. It looks weirdly like the ESPN stats pages except everyone here is committing a crime.

### Eli Pelor
![](/images/100Days/Day58/airdrops.png)

elipelor.com, which is linked to in that email address down at the bottom, is a webpage dedicated to crypto airdrops. Crypto airdrops are when new coins do an Initial Coin Offering (remember those from day 29?) and give away a few dozen or so of their newly minted, totally worthless tokens to whoever signs up for them. elipelor.com helps keep track of those free giveaways to let you know when you can get your mitts on some free digiswag.
![](/images/100Days/Day58/elipelor.png)
How is this all related? I think it's being run by someone in the hacking collective. And I don't think it's entirely aboveboard. As I was trying to get to the "about us page" _I was briefly redirected out-of-site_ to a site called blacklink.us.
![](/images/100Days/Day58/blacklink.png)
Black Link monetizes links by capturing you on a page and making you wait while you get serviced a bunch of ads meant to look like "proceed to your content" buttons and probably skim off some of your CPU for crypto mining. They then pay anyone who hosts one of their links some money for every 1000 clicks they get, prorated to how wealthy the country of origin of the clicker is.

It's real bottom feeder type stuff. Which puts it only one ladder rung above [Outbrain](https://www.outbrain.com/). See you tomorrow.
