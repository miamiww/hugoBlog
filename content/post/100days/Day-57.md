+++
title = "Shodan Stories Day 57: Shodaning Myself, Ye Olde Telnet Service, and the Weather Underground"
date = 2019-03-01T17:30:12-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Yes today I Shodaned myself. Nothing shows up for my full name, thankfully, but "alden" has a lot of results.

## The Weather Underground on 35.160.169.47
I picked a result in Boardman, Oregon, largely because of how charming it was. It's just a [telnet](https://en.wikipedia.org/wiki/Telnet) server, running on port 23 and mirrored on port 3000. You almost never see telnet anymore these days, since it's been primarily replaced with the much more secure ssh. Here I am loggin in via `netcat`
```
➜  sandbox git:(master) ✗ nc 35.160.169.47 23
------------------------------------------------------------------------------
*               Welcome to THE WEATHER UNDERGROUND telnet service!            *
------------------------------------------------------------------------------
*                                                                            *
*   National Weather Service information provided by Alden Electronics, Inc. *
*    and updated each minute as reports come in over our data feed.          *
*                                                                            *
*   **Note: If you cannot get past this opening screen, you must use a       *
*   different version of the "telnet" program--some of the ones for IBM      *
*   compatible PC's have a bug that prevents proper connection.              *
*                                                                            *
*           comments: jmasters@wunderground.com                              *
------------------------------------------------------------------------------

Press Return to continue:

```
[The Weather Underground](https://www.wunderground.com/)! I'd actually heard of them before, they were the first weather service attached to the internet for the use of the public. Apparently it [started as a telnet service](https://en.wikipedia.org/wiki/Weather_Underground_(weather_service)#History) back in 1991, became a fairly successful weather company and highly visited website by the mid 00s, and is now owned by IBM. But the telnet service stays on. I like that.

And now I see why this result came up when I searched for my name, it's provided by [Alden Electronics](http://www.alden.com/), a manufacturer of all kinds of weather related gadgets.
![](/images/100Days/Day57/aelectronics.png)
I'd come across them before, because they own alden.com, a domain name that I'd clearly benefit from more. Figuring I'd give the old telnet service a spin I checked the forecast for New York City.
```
Press Return for menu
or enter 3 letter forecast city code-- NYC
Weather Conditions at 04:51 PM EST on 01 Mar 2019 for New York JFK, NY.
Temp(F)    Humidity(%)    Wind(mph)    Pressure(in)    Weather
========================================================================
  36          73%         EAST at 7       30.28      Overcast

Forecast for New York, NY
421 PM EST Fri Mar 1 2019

...Winter Weather Advisory in effect until noon EST Saturday...

.Tonight...Sleet, snow. Snow and sleet accumulation of 2 to
4 inches. Lows in the lower 30s. Northeast winds 10 to 15 mph.
Chance of precipitation near 100 percent.
.Saturday...Cloudy. A chance of rain and snow in the morning,
then a slight chance of light rain and light snow in the
afternoon. Highs around 40. North winds 10 to 15 mph with gusts
up to 25 mph. Chance of precipitation 40 percent.
.Saturday night...Mostly cloudy. Lows in the lower 30s. West
winds 5 to 10 mph.
.Sunday...Partly sunny in the morning, then mostly cloudy with
rain likely in the afternoon. Highs in the lower 40s. Northwest
winds 5 to 10 mph, becoming southeast in the afternoon. Chance of
rain 60 percent.
   Press Return to continue, M to return to menu, X to exit:
```

Snow tonight! I hadn't realized. There's actually a fair bit you can do.

```
WEATHER UNDERGROUND MAIN MENU
******************************
1) U.S. forecasts and climate data
2) Canadian forecasts
3) Current weather observations
4) Ski conditions
5) Long-range forecasts
6) Latest earthquake reports
7) Severe weather
8) Hurricane advisories
9) Weather summary for the past month
10) International data
11) Marine forecasts and observations
12) Ultraviolet light forecast
X) Exit program
C) Change scrolling to screen
H) Help and information for new users
?) Answers to all your questions
  Selection:?

WEATHER UNDERGROUND HELP AND INFORMATION MENU
---------------------------------------------
1) How to connect
2) How the Weather Underground works
3) How to set up your own telnet service
M) Return to main menu
X) Exit program
  Selection:3

No data available.
/wx/data/DAT/help3.doc
WEATHER UNDERGROUND HELP AND INFORMATION MENU
---------------------------------------------
1) How to connect
2) How the Weather Underground works
3) How to set up your own telnet service
M) Return to main menu
X) Exit program
  Selection:
```
Unfortunately some of their help pages have gone missing. I'd have loved their guide on how to set up your own telnet service, but I might have been the first person to check that in several years. I'm not surprised it's gotten lost somehow.

I guess I'll have to find some other guide. See you tomorrow.
