---
author: alden
categories:
- Physical Computing
date: 2017-10-18
guid: https://www.alden.life/?p=245
id: 245
title: Making a Controller for My P5 Game
url: /2017/10/18/making-a-controller-for-my-p5-game/
---

(note all the code for these projects can be viewed on my Github [here](https://github.com/miamiww/PhysicalComputing/tree/master/Week6/joystickP5) though I will make specific references to scripts down below).

One of my P5 projects that I am the happiest with is an interactive poetry/anti-game game that involves corralling a ball with the cursor to reveal a narrative. I decided I wanted to replace the mouse and cursor with a joystick, and that I wanted to use node, [express](https://expressjs.com/), and a websocket to interface between P5 and the arduino.

<img class="wp-image-246 size-full aligncenter" src="https://www.alden.life/wp-content/uploads/2017/10/giphy.gif" alt="" width="480" height="324" />

I started out by adapting the [SerialInOut example code](https://github.com/miamiww/PhysicalComputing/blob/master/Week6/joystickP5/AnalogInOutSerial/AnalogInOutSerial.ino) for arduino to work for a joystick since the example uses a potentiometer and a joystick is just two potentiometers and a switch. Making those changes I wrote [this code](https://github.com/miamiww/PhysicalComputing/blob/master/Week6/joystickP5/Joystick/Joystick.ino) for outputting the joystick readings to serial. I had some trouble setting wiring the joystick initially but Aiden helped me out. Also I read on a now forgotten stack exchange that INPUT_PULLUP is necessary for setting the pinmode on digital ins that are going over serial, but I didn&#8217;t understand why that is the case.

<img class="wp-image-250  aligncenter" src="https://www.alden.life/wp-content/uploads/2017/10/joystick-2-e1508300755163-1024x1024.jpg" alt="" width="501" height="501" srcset="https://www.alden.life/wp-content/uploads/2017/10/joystick-2-e1508300755163-1024x1024.jpg 1024w, https://www.alden.life/wp-content/uploads/2017/10/joystick-2-e1508300755163-150x150.jpg 150w, https://www.alden.life/wp-content/uploads/2017/10/joystick-2-e1508300755163-300x300.jpg 300w, https://www.alden.life/wp-content/uploads/2017/10/joystick-2-e1508300755163-768x768.jpg 768w" sizes="(max-width: 501px) 100vw, 501px" />

Before trying to figure out how to integrate the serial readings into my game/poem script I connected it to a very quick example [here](https://github.com/miamiww/PhysicalComputing/blob/master/Week6/joystickP5/public/sketch.js) which you can see in the first gif above. I&#8217;d used node and websockets before but I didn&#8217;t really remember them very well so it took me a pretty long time to get off the ground. I made use of some code that I had from [Mark Hellar](http://grayarea.org/community-entry/mark-hellar/) from when I was at Grey Area, which is why I ended up using express.

<img class="aligncenter wp-image-249 size-full" src="https://www.alden.life/wp-content/uploads/2017/10/NOtGood.gif" alt="" width="480" height="300" />

Once I figured out the example worked I went about redoing my P5 project to take the serial input. It didn&#8217;t take very long, I just replaced the mouseX and mousePressed variables with the respective inputs from the joystick. I intentionally made it so that you couldn&#8217;t see the player&#8217;s &#8220;cursor&#8221;, I wanted discovering the relationship between what the player was doing and the motion of the ball to be didactic and not immediately clear (so that you have to play around with the joystick before you figure out what is going on).
