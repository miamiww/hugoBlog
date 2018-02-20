---
author: alden
categories:
- Physical Computing
date: 2017-11-15
guid: http://www.alden.life/?p=286
id: 286
title: Haunted Dollhouse Planning
url: /2017/11/15/haunted-dollhouse-planning/
---

<img class="alignnone wp-image-295 size-large" src="http://www.alden.life/wp-content/uploads/2017/11/2017-11-20-14.34.48-2-e1511206799322-706x1024.jpg" alt="" width="706" height="1024" srcset="http://www.alden.life/wp-content/uploads/2017/11/2017-11-20-14.34.48-2-e1511206799322-706x1024.jpg 706w, http://www.alden.life/wp-content/uploads/2017/11/2017-11-20-14.34.48-2-e1511206799322-207x300.jpg 207w, http://www.alden.life/wp-content/uploads/2017/11/2017-11-20-14.34.48-2-e1511206799322-768x1113.jpg 768w" sizes="(max-width: 706px) 100vw, 706px" />

At this point I have gotten the basic Google home API working on my raspberry pi and have started manipulating the methods of interaction (changing the trigger word, changing the voices) and have started to work on building a specific Google home Action. Still to do is build the haunted dollhouse enclosure. Since the basic first interaction I want users to have with the haunted doll is to knock on the dollhouse door, I wanted to first set up a basic knock and open circuit.

<img class="alignnone wp-image-287 size-full" src="http://www.alden.life/wp-content/uploads/2017/11/BasicPiezo_schem.png" alt="" width="981" height="858" srcset="http://www.alden.life/wp-content/uploads/2017/11/BasicPiezo_schem.png 981w, http://www.alden.life/wp-content/uploads/2017/11/BasicPiezo_schem-300x262.png 300w, http://www.alden.life/wp-content/uploads/2017/11/BasicPiezo_schem-768x672.png 768w" sizes="(max-width: 981px) 100vw, 981px" />

The piezo would be connected to the inside of the door and the motor underneath or above the door, rotating an axle that controls the door hinges. I am not sure if a servo is best for this or if there is a better motor for this application. The piezo would detect the knock (any kind of knock should do) and trigger the motor to open the door.

Beyond this very basic interaction I have a few different ideas. The aesthetics and interaction in my mind are beginning to push into [Zoltar](https://www.youtube.com/watch?v=U8Jdhh1L70Y) territory, so I was thinking of adding a thermal printer printout of whatever fortune or advice the doll is giving. Additionally I would like to replace the trigger word with the knock, i.e. to connect the arduino to the pi and trigger the pi to start listening for a question once a user has knocked on the door. Additionally I would like to incorporate some movement in the doll, that was the biggest feedback that I received at user testing. I think an easy start would be to put two LEDs in the eyes so that the eyes light up. From there, with time and resources I could add additional movements, such as a head or arm movement.
