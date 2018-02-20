---
author: alden
categories:
- Physical Computing
date: 2017-09-20
enclosure:
- |
  http://www.alden.life/wp-content/uploads/2017/09/2017-09-19-14.42.04.mov
  19374672
  video/quicktime
- |
  http://www.alden.life/wp-content/uploads/2017/09/2017-09-19-14.56.05.mov
  21498326
  video/quicktime
guid: http://www.alden.life/?p=144
id: 144
title: Servo Switch
url: /2017/09/20/servo-switch/
---

[Pen Switch](http://www.alden.life/wp-content/uploads/2017/09/2017-09-19-14.42.04.mov)

My first switch was very simple, I wanted to incorporate elements outside of the traditional breadboard circuit so <span style="font-size: 1rem;">I used the metal part of a pen to connect two circuit elements and complete a circuit and light up an LED. </span>

[Servo Switch](http://www.alden.life/wp-content/uploads/2017/09/2017-09-19-14.56.05.mov)

I really wanted to get my hands into programming the arduino so I next made a switch that involves stringing a resistor into the arm of a small servo motor and using the arduino to control the movements of the motor so that it completes a circuit and lights up an LED. It&#8217;s a really bad switch on its own because it just cycles on and off so I added a button that lets you stop the motion of the servo motor when it is pressed (kind of jankily by mixing up the ground and the communication signals the arduino is sending to the servo). It starts moving again as soon as you unpress the button so if you want the LED to stay lit you have to keep your finger on the button. To move the servo I just used the SERVO\_SWEEP\_INO example code in the arduino IDE.

<img class="alignnone wp-image-147 size-medium" src="http://www.alden.life/wp-content/uploads/2017/09/2017-09-19-15.04.03-e1505923627900-225x300.jpg" alt="" width="225" height="300" srcset="http://www.alden.life/wp-content/uploads/2017/09/2017-09-19-15.04.03-e1505923627900-225x300.jpg 225w, http://www.alden.life/wp-content/uploads/2017/09/2017-09-19-15.04.03-e1505923627900-768x1024.jpg 768w" sizes="(max-width: 225px) 100vw, 225px" />
