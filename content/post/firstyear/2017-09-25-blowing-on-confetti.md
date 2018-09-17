---
author: alden
categories:
- Uncategorized
date: 2017-09-25
guid: https://www.alden.life/?p=155
id: 155
title: Blowing on Confetti
url: /2017/09/25/blowing-on-confetti/
---

I&#8217;ve been wanting to recreate the experience of playing with confetti, this is one prototype for interacting with confetti by &#8220;blowing&#8221; on it with the mouse.

[<img class="alignnone wp-image-156 size-full" src="https://www.alden.life/wp-content/uploads/2017/09/Confetti.png" alt="" width="600" height="600" srcset="https://www.alden.life/wp-content/uploads/2017/09/Confetti.png 600w, https://www.alden.life/wp-content/uploads/2017/09/Confetti-150x150.png 150w, https://www.alden.life/wp-content/uploads/2017/09/Confetti-300x300.png 300w" sizes="(max-width: 600px) 100vw, 600px" />](https://alpha.editor.p5js.org/full/H1vE2TIoZ)

Right now they kind of jiggle around expectantly, this was to meet the &#8220;one element that moves independently of the mouse&#8221; part of the homework.  Getting the confetti to move realistically when blown has been a pain, right now it jumps around semi-randomly, which gives a good imitation of a scattering effect but the motion is discontinuous and unnatural. Ideally I&#8217;d like other kinds of interactions, like brushing it away or being able to tilt the canvas and have it move to one side.

&nbsp;

I wanted to functionalize my code so that I could use it to pile confetti on top of whatever I want to in the future. First I populate an array with a list of coordinates, and then I give those coordinates attributes like shape, color, and movement. Clickthrough the picture below to get to the code, where I have more detailed comments explaining what I did.

<a style="background-color: #ffffff; font-size: 1rem;" href="https://alpha.editor.p5js.org/alden/sketches/H1vE2TIoZ"><img class="alignnone wp-image-157 size-full" src="https://www.alden.life/wp-content/uploads/2017/09/DidIt.png" alt="" width="600" height="600" srcset="https://www.alden.life/wp-content/uploads/2017/09/DidIt.png 600w, https://www.alden.life/wp-content/uploads/2017/09/DidIt-150x150.png 150w, https://www.alden.life/wp-content/uploads/2017/09/DidIt-300x300.png 300w" sizes="(max-width: 600px) 100vw, 600px" /></a>
