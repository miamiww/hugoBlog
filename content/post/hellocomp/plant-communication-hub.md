+++
title = "Leaf Town: Plant Communication Hub"
date = 2018-10-19T18:50:48-04:00
draft = false
tags = []
categories = ["hello computer"]
+++
![](/images/HelloComp/LeafTown/SSHBanner.png)
In making this project I had on my mind both the kind of joy of speaking to non-humans and feeling understood, generating a level of closeness that can feel deep yet uncomplicated, and the kind of snake-oilish claims that some researchers in the AI community make about their work. Naturally these thoughts led me to start making a device that would allow users to speak directly with their plants and have the plants speak back. I set about creating some kind of speculative fiction about the inner lives of my own plants and then scripting that fiction into speech interactions using a Raspberry Pi with the [Google AIY Voice hat](https://aiyprojects.withgoogle.com/voice/).
![](/images/HelloComp/LeafTown/TheHub.jpg)
The cats in the above image are purely decorative. For the look and feel of the device I wanted it to look fairly nondescript in a home context, evoke associations with plants and plant care, and then appear somewhat bizarre on closer inspection, to evoke a sense of estrangement. I decided to use a terra cotta pot for housing because of its familiarity and clear associations with houseplants, and to seal the top with a round of astroturf. And then I decided to name it Leaf Town because I thought the name was curiously unlike the names for tech products of today (maybe in the future such names will be different), and almost jarringly innocent, like it could be the name for a children's TV show. Of course, the personality I had developed for my plants was itself very innocent, they are very cute, so the name fit with their general vibe. For their voice I liked the slightly more robotic version of the Google assistant voice that came as a default, as it is again both familiar and strange at the same time.
![](/images/HelloComp/LeafTown/Wires.jpg)
I wanted lots of wiring to come out the bottom, like an [Evan Roth piece](http://www.evan-roth.com/work/kites-and-websites/) or something. No opacity yet all opacity.
![](/images/HelloComp/LeafTown/Inside.jpg)
Placing the microphone inside of the pot creates some "hearing" issues, but I scripted the interactions in such a way that if the plant doesn't hear any speech it will respond in an ambiguous enough way that it could have been a response to anything.
![](/images/HelloComp/LeafTown/Gregorio.jpg)
I also wanted wiring running to the plants that the hub was communicating with, detailing in this fiction that of course plants cannot communicate via wifi and would need a direct link into their roots.
![](/images/HelloComp/LeafTown/TheButton.jpg)
One thing that I don't like about my implementation is needing a button in order to start the device listening for speech. If I were to give this more polish, I would like to use a pressure sensor in the astroturf that could tell when a plant or someone's hand was on top of it, and have the device start autolistening whenever it detects pressure.

Here you can watch me interviewing one of my plants, Gregorio, using the device:
{{< vimeo 297114740 >}}
The abover video can be downloaded directly [here](https://www.dropbox.com/s/fc8fyvpkl43jew1/EditedPlantTalk.mov?dl=0)

All code for the project can be found [on my Github here](https://github.com/miamiww/HelloComputer/tree/master/plant_communication_hub)
