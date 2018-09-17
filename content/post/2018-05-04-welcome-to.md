---
author: alden
categories:
- electronic text
date: 2018-05-04
title: Welcome To
url: /2018/05/04/welcome-to
---
![*record scratch* yup, that's me. I bet you're wondering how I ended up in this situation](/images/1O3A0114.JPG)
I have been thinking about a completely automated conference talk since I saw Hito Steyerl and Wendy Chun give a talk at The Guggenheim for Hito's book launch in January. Much of the content of their conversation had to do with economies of labor in art, economies of presence in art, and of the demands on artists and their time and of the place of the 'artist talk' within the art labor economy. This discussion of the value of presence resonated with me as I feel constant pulls on my attention and presence from all the devices and pressures for success and a thousand bits of regret for not doing enough or reminders or notifications in a constant blender of anxiety. Blah blah blah everyone's phone is constantly demanding that they be in 18 places at once. My ideal product was a talk in which I become merely a vessel for an automated process, and I feel as though I more or less accomplished this goal with this piece.

If you don't want to read too much about the process and just want the good stuff, you can see an example of a generated slide deck [here](https://docs.google.com/presentation/d/1FGxM85ikyp8bNPNWEgepR7e0oRgiek6f-uUo-fsyyMs/edit?usp=sharing), or look over my code [here](https://github.com/miamiww/ElectronicText/tree/master/final_project). Of course a performance is only in the ephemeral doing.

[![Duty Free Art](http://images.e-flux-systems.com/43924124-F0B7-4856-8353-33447CDBCF88.jpg,2000)](http://www.e-flux.com/program/170589/double-u-s-book-launch-nbsp-duty-free-art-nbsp-and-supercommunity-at-the-guggenheim/)
My first first step in the process was to build a corpus of various conference talks and stitch them together using markov chains of various character and word lengths. With my initial undertakings I tended to prefer 2 word chains.
```
Time’s unity is asymmetric: the past present can only
be understood for what it was and wasn’t
(qua condition and projection to the dead: parents
and grandparents and so forth.
I can create and meet a set of established
stereotypes of myself.
```
I also tried recurrent neural networks using the [textgennr](https://github.com/minimaxir/textgenrnn) module, but the weird results were too weird and the less weird results weren't weird enough.
```
Junkant-is to be administering its makes endlycrace,
its authenticstical extend the air of the decends,
the practice of derks makes a precious for who does
not and templated to provide particicists
```
or
```
The aurality of the present and the present and the
present and the present and the present and the
present and the projects of the present and the
projection of the projection of the future of the
```
My real interest in this was in then using a [reaction prediction neural network](https://github.com/minimaxir/reactionrnn) to build instructions for the audience's interpretation of the piece. But I ended up getting swept up in what I can only refer to as Alden's Big Webdriver Moment of 2018, where I learned about webdrivers and wanted to use them for everything.
![slidebot](/images/lilslidebot.gif)
Using a webdriver led me to start scraping slides from [slideshare.net](https://www.slideshare.net/) to put them together into a presentation, and the audience direction pieces just didn't feel integrateable into the [snappy/cheesy](https://www.youtube.com/watch?v=gOa1fK5USXk) direction I had started going into.
