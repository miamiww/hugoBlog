+++
title = "Shodan Stories Day 51: Keeping Abreast of the Hyperlocal Weather in Uppsala, Yawcam, and Multinational Pest Control"
date = 2019-02-23T07:29:11-08:00
draft = false
tags = []
categories = ["100 days"]
+++

A quick webcam day as I was busy with a conference most of the day.

## A Yawcam on 85.224.37.79
This time I went looking for ["yawcam"](https://www.yawcam.com/), a webcam server software whose name stands for Yet Another Webcam.
![](/images/100Days/Day51/yawcam.png)

Like most free DIY webcam servers the default seems to be "completely insecure", and I found quite a few interesting cameras, but chose one in Sweden that was running on port 8888.
![](/images/100Days/Day51/weather.png)
I love this because this person has so clearly come up with the exact perfect hack for their needs. Why do they remotely need to see the temperature and weather of this room I do not know, but they are able to from wherever they might be. In the background however I see what seems to be a child's room, a guess I make only because of the stuffed animal on the floor.

Greater questions arise. Is this actually the indoor temperature? There is an image of a raincloud on it and the word FORECAST (you typically don't get an indoor forecast), but these temperatures don't seem to be the forecast for Uppsala Sweden, where it's a fair bit colder than 15C for the next few days. On the bottom the device has the name "Anticimex". Anticimex is a [multinational pest control company](https://en.wikipedia.org/wiki/Anticimex), which doesn't seem like they should be manufacturing temperature sensors.
![](/images/100Days/Day51/thermostat.png)
It looks like in Sweden's Anticimex retailer _does_ have different kind of temperature sensors, but no weather forecast device, and nothing that looks just like this.

Maybe it's just an older model? Using the [Internet Archive](https://web.archive.org/web/20180105091953/https://shop.anticimex.com/vatten-och-fukt/digitalfuktmatare) I was able to track down this exact device, a multi zone weather station made in conjunction with [Oregon Scientific](https://store.oregonscientific.com/us/).
![](/images/100Days/Day51/older.png)


No explanation for why it calls it a "forecast", but it seems to be for measuring multiple rooms in your house, coming with several sensors and the one digital display.

I guess it wasn't such a quick one after all. See you tomorrow.
