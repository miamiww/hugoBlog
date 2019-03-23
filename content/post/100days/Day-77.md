+++
title = "Shodan Stories Day 77: Compressing Natural Gas in West Virginia"
date = 2019-03-22T20:17:53-04:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I saw a search on Shodan just for "compressor station". Turns out that [compressor stations](https://en.wikipedia.org/wiki/Compressor_station) are facilities for compressing natural gas so that it can be transported through a pipeline, and that a natural gas pipeline will frequently have many compressor stations to help keep things moving.

## Natural Gas Compressor Station on 184.13.121.30
There were only 8 results, and I chose one in Fairmont, West Virginia because it was using [Red Lion Controls](https://www.redlion.net/), just like the oil field I found on day 32. It was running the Red Lion protocol on port 789, and two webservers on 8081 and 8083. The 8081 webserver gives a 401 no authentication error.
```
HTTP/1.1 401 Unauthorized
Content-Type: text/html
WWW-Authenticate: Basic realm="AR Midstream: Goff Compressor Station",
Cache-Control: no-cache, no-store
Connection: Keep-Alive
Content-Length: 435
```
That's where the "compressor station" result comes in. With a little Googling I found that [the Goff compressor station is in Harrison county West Virginia](https://dep.wv.gov/daq/Documents/September%202017%20Applications/033-00187_APPL_G35-D107F.pdf). In fact I found out quite a bit about it. In West Virginia all pipeline permitting is part of the public record, including the exact GPS coordinates of the facility.
![](/images/100Days/Day77/maps.png)
This is as close as I could get to it on Google maps, it's just down that road. I'd have imagined that there would be more of a to-do about it, like a more serious gate, but then I checked the date on the maps image and found that it was from all the way back in 2009. The facility was only permitted in 2017. Who knows what lay behind this road in 2009. I found a blog post from a guy [investigating the pipeline in 2018](http://www.frackcheckwv.net/2018/09/22/fullstream-goff-connector-pipeline-is-a-sneaking-snake-on-the-wv-landscape/), and he said that he went to about this very area and found two guards, so I assume things have changed.

The permitting all indicated that the facility is owned by a company called [Arsenal Midstream](https://www.arsenalresources.com/operations/midstream/), and the webserver on 8083 confirmed that. It is the same kind of data logger interface we saw for Red Lion on day 32.
![](/images/100Days/Day77/firstlook.png)
I believe that DeHy means dehydration, in this case a process called [glycol dehydration](https://en.wikipedia.org/wiki/Glycol_dehydration), which is used to remove water from natural gas so that it can be processed, compressed, and added to a pipeline. The logs all had to do with things like pump control, temperature, water percentage, flow rates. You know, typical things.
![](/images/100Days/Day77/remoteview.png)
The remote view was this login that I can assume is also on a physical screen out there in the West Virginia woods.

While I'm not able to really do anything, that I am able to get logs from the station seems a little troubling. But maybe the convenience in this case is worth it: you can share the logging and management widely so that if something goes wrong you can easily share data with a repair crew quickly without needing to get them authorization. See you tomorrow.
