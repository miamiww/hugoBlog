+++
title = "Shodan Stories Day 36: A Sick Beard in Hilversum, Usenet Is Still Around, Torrenting SuperUsers, and How Much of the Internet Is Just People Trying to Watch TV?"
date = 2019-02-08T22:40:09-05:00
draft = false
tags = []
categories = ["100 days"]
+++

The Shodan recent searches is a well that never runs dry. Today I saw someone searching for "Sickbeard". What could that possibly be??

## Sickbeard TV on 85.145.200.210
The search was named Sickbeard but the actual search was for "CherryPy/3.2.0rc1 This resource can be found at". Looking into it, [CherryPy](https://cherrypy.org/) is a python based framework for running webapps. It looks useful and I think I'll log it into my toolkit for a later project. But on with Sickbeard, I decided to go for the first result I found as it is in the Netherlands and I was hoping for interesting Netherlands TV. Yes TV! I did a brief Googling and found that Sickbeard was some kind of TV thing but didn't dive that deep yet.
![](/images/100Days/Day36/sickbeard.png)
This server was running the Sickbeard webapp on port 7071. I was immediately dissapointed to see that the first TV show listed was The Big Bang Theory. Like come on. Game of Thrones?? Everybody Loves Raymond??? What a letdown. At least they're watching The O.C.
![](/images/100Days/Day36/tv.png)
Unlike a lot of systems like this that I've found I couldn't interact with any of the media in any way, it seems to be a management system for downloads rather than a media streaming server.


Actually reading about [Sickbeard on its website](http://sickbeard.com/index.html) I found that it actually has an extremely niche use-case. Sickbeard monitors posts in [Usenet newsgroups](https://en.wikipedia.org/wiki/Usenet) dedicated to TV show torrents, grabs the torrent files for the list of shows you've given it, and then gives those torrent files over to a torrent client.

Watching TV shows for free was a hell of a lot harder back in my day. The good old days, when you'd have to set up a [Seedbox](https://en.wikipedia.org/wiki/Seedbox) just to have a good enough ratio to get on some 1337 Torrenting message board, and then beg and plead for people to upload the version of [Naruto](https://en.wikipedia.org/wiki/Naruto) subbed by your favorite subbing group, you know, the one that used Real Swears, and then sit and wait for 19 hours while the episode downloaded with the one uploader probably on a DSL modem somewhere in the Balkans. Those were truly the days of miracle and wonder.

I'm kidding, I never watched Naruto. I was more into [Bleach](https://en.wikipedia.org/wiki/Bleach_(TV_series)). See you tomorrow.
