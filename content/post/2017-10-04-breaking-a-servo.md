---
author: alden
categories:
- Physical Computing
date: 2017-10-04
guid: https://www.alden.life/?p=208
id: 208
title: Breaking A Servo?
url: /2017/10/04/breaking-a-servo/
---

I wanted to make a project that would display a dubiously motivational message each time I sat at my home office desk. To start off I used a HC-SR04 ping distance sensor and attached a pin with a message (in this case a pin I got at the art book fair) to a little SG90 micro servo motor. I initially tried to map the distance readings of the HC-SR04 to the angle of the servo motor, but it was too noisy and the servo jittered around quickly (you can see that code commented out below).

<img class="alignnone size-medium wp-image-212" src="https://www.alden.life/wp-content/uploads/2017/10/2017-10-04-11.17.06-e1507130751661-291x300.jpg" alt="" width="291" height="300" srcset="https://www.alden.life/wp-content/uploads/2017/10/2017-10-04-11.17.06-e1507130751661-291x300.jpg 291w, https://www.alden.life/wp-content/uploads/2017/10/2017-10-04-11.17.06-e1507130751661-768x792.jpg 768w, https://www.alden.life/wp-content/uploads/2017/10/2017-10-04-11.17.06-e1507130751661-993x1024.jpg 993w" sizes="(max-width: 291px) 100vw, 291px" />

After that I tried running it as an if/then statement, where the servo would change positions if the distance sensor recorded a short distance. However, the servo didn&#8217;t change position even as I watched the distance go below the threshold on the serial monitor. Instead it stayed in one place making a really awful noise and getting hotter until it stopped moving at all. After that it wouldn&#8217;t move at all even for simpler movements like the servo sweep example code, leading me to think that it was broken. However I tried it again after it had cooled down and it worked fine, but just still not for the application I wanted.

<img class="alignnone wp-image-213 size-large" style="font-size: 1rem;" src="https://www.alden.life/wp-content/uploads/2017/10/2017-10-04-11.24.57-e1507130951760-1024x1024.jpg" alt="" width="739" height="739" srcset="https://www.alden.life/wp-content/uploads/2017/10/2017-10-04-11.24.57-e1507130951760-1024x1024.jpg 1024w, https://www.alden.life/wp-content/uploads/2017/10/2017-10-04-11.24.57-e1507130951760-150x150.jpg 150w, https://www.alden.life/wp-content/uploads/2017/10/2017-10-04-11.24.57-e1507130951760-300x300.jpg 300w, https://www.alden.life/wp-content/uploads/2017/10/2017-10-04-11.24.57-e1507130951760-768x768.jpg 768w" sizes="(max-width: 739px) 100vw, 739px" />

<pre>You can see the code here:

<span style="color: #5e6d03;">#include</span> <span style="color: #434f54;">&lt;</span><b><span style="color: #d35400;">Servo</span></b><span style="color: #434f54;">.</span><span style="color: #000000;">h</span><span style="color: #434f54;">&gt;</span>

<b><span style="color: #d35400;">Servo</span></b> <span style="color: #000000;">myServo</span><span style="color: #000000;">;</span>

<span style="color: #00979c;">const</span> <span style="color: #00979c;">int</span> <span style="color: #000000;">trigPin</span> <span style="color: #434f54;">=</span> <span style="color: #000000;">13</span><span style="color: #000000;">;</span>
<span style="color: #00979c;">const</span> <span style="color: #00979c;">int</span> <span style="color: #000000;">echoPin</span> <span style="color: #434f54;">=</span> <span style="color: #000000;">12</span><span style="color: #000000;">;</span>
<span style="color: #00979c;">const</span> <span style="color: #00979c;">int</span> <span style="color: #000000;">servoPin</span> <span style="color: #434f54;">=</span> <span style="color: #000000;">6</span><span style="color: #000000;">;</span>
<span style="color: #00979c;">int</span> <span style="color: #000000;">servoAngle</span><span style="color: #000000;">;</span>

<span style="color: #00979c;">long</span> <span style="color: #000000;">duration</span><span style="color: #000000;">;</span>
<span style="color: #00979c;">int</span> <span style="color: #000000;">distance</span><span style="color: #000000;">;</span>

<span style="color: #00979c;">void</span> <span style="color: #5e6d03;">setup</span><span style="color: #000000;">(</span><span style="color: #000000;">)</span> <span style="color: #000000;">{</span>
  <span style="color: #d35400;">pinMode</span><span style="color: #000000;">(</span><span style="color: #000000;">trigPin</span><span style="color: #434f54;">,</span> <span style="color: #00979c;">OUTPUT</span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
  <span style="color: #d35400;">pinMode</span><span style="color: #000000;">(</span><span style="color: #000000;">echoPin</span><span style="color: #434f54;">,</span> <span style="color: #00979c;">INPUT</span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
  <b><span style="color: #d35400;">Serial</span></b><span style="color: #434f54;">.</span><span style="color: #d35400;">begin</span><span style="color: #000000;">(</span><span style="color: #000000;">9600</span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
  <span style="color: #000000;">myServo</span><span style="color: #434f54;">.</span><span style="color: #d35400;">attach</span><span style="color: #000000;">(</span><span style="color: #000000;">servoPin</span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
<span style="color: #000000;">}</span>

<span style="color: #00979c;">void</span> <span style="color: #5e6d03;">loop</span><span style="color: #000000;">(</span><span style="color: #000000;">)</span> <span style="color: #000000;">{</span>
  <span style="color: #000000;">myServo</span><span style="color: #434f54;">.</span><span style="color: #d35400;">write</span><span style="color: #000000;">(</span><span style="color: #000000;"></span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
  <span style="color: #d35400;">digitalWrite</span><span style="color: #000000;">(</span><span style="color: #000000;">trigPin</span><span style="color: #434f54;">,</span> <span style="color: #00979c;">LOW</span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
  <span style="color: #d35400;">delayMicroseconds</span><span style="color: #000000;">(</span><span style="color: #000000;">2</span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
  <span style="color: #d35400;">digitalWrite</span><span style="color: #000000;">(</span><span style="color: #000000;">trigPin</span><span style="color: #434f54;">,</span> <span style="color: #00979c;">HIGH</span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
  <span style="color: #d35400;">delayMicroseconds</span><span style="color: #000000;">(</span><span style="color: #000000;">10</span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
  <span style="color: #d35400;">digitalWrite</span><span style="color: #000000;">(</span><span style="color: #000000;">trigPin</span><span style="color: #434f54;">,</span> <span style="color: #00979c;">LOW</span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
  <span style="color: #000000;">duration</span> <span style="color: #434f54;">=</span> <span style="color: #d35400;">pulseIn</span><span style="color: #000000;">(</span><span style="color: #000000;">echoPin</span><span style="color: #434f54;">,</span> <span style="color: #00979c;">HIGH</span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
  <span style="color: #000000;">distance</span> <span style="color: #434f54;">=</span> <span style="color: #000000;">duration</span> <span style="color: #434f54;">*</span> <span style="color: #000000;">0.034</span> <span style="color: #434f54;">/</span> <span style="color: #000000;">2</span><span style="color: #000000;">;</span>
  <b><span style="color: #d35400;">Serial</span></b><span style="color: #434f54;">.</span><span style="color: #d35400;">print</span><span style="color: #000000;">(</span><span style="color: #005c5f;">"Distance: "</span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
  <b><span style="color: #d35400;">Serial</span></b><span style="color: #434f54;">.</span><span style="color: #d35400;">println</span><span style="color: #000000;">(</span><span style="color: #000000;">distance</span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>

  <span style="color: #5e6d03;">if</span><span style="color: #000000;">(</span><span style="color: #000000;">distance</span> <span style="color: #434f54;">&lt;</span> <span style="color: #000000;">10</span><span style="color: #000000;">)</span> <span style="color: #000000;">{</span>
    <span style="color: #000000;">myServo</span><span style="color: #434f54;">.</span><span style="color: #d35400;">write</span><span style="color: #000000;">(</span><span style="color: #000000;">90</span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
  <span style="color: #000000;">}</span> <span style="color: #5e6d03;">else</span> <span style="color: #000000;">{</span>
    <span style="color: #000000;">myServo</span><span style="color: #434f54;">.</span><span style="color: #d35400;">write</span><span style="color: #000000;">(</span><span style="color: #000000;"></span><span style="color: #000000;">)</span><span style="color: #000000;">;</span>
  <span style="color: #000000;">}</span>



  <span style="color: #434f54;">// int servoAngle = map(distance, 0, 30, 0, 179);</span>
  <span style="color: #434f54;">//  myServo.write(servoAngle);</span>

<span style="color: #000000;">}</span>

</pre>
