+++
title = "RESTful VJing"
date = 2018-11-12T22:46:34-05:00
draft = false
tags = []
categories = ["understanding networks"]
+++
[Beverly](https://itp.beverlychou.com/) and I decided to work on a quick VJing system. We started out doing research and interviewed a few people on the floor to ask them what they thought made for good VJing, and what made for bad VJing. The most consistent thing we heard was that the visuals should match the mood and timing of the music. Since beat syncing the visuals to the music might be hard with REST we decided to have two "modes" for the system, GIF mode and visuals mode. GIF mode can be activated with a POST and will query giphy.com with a given search term and then display a random GIF from that search result. So in activating GIF mode a search word would also need to be provided, either typed out or speech to text interpreted over a microphone.
![](/images/UnderNet/restful.jpg)
Visuals mode would feature moving shapes over a color background, a bit like a very 1990s pattern signifying multimedia.
![](https://cdn.dribbble.com/users/258978/screenshots/4632896/90_s-dribbble.png)
For these the controls would be over

* shape speed
* background color
* shape color
* shapes being currently displayed (ellipse, squiggle, triangle, rectangle, arc)

Beverly drew a very nice diagram of the whole system:
![](https://itp.beverlychou.com/assets/und-networks/REST-system-diagram-for-VJ.jpg)
