---
layout:     post
comments: 	true
title:      "Word Clock"
subtitle:   "Arduino powered word clock"
date:       2015-03-30 16:00:00
author:     "Josh Fermin"
header-img: "img/blog/rgbledstrip.jpg"
---

<h2 class="section-heading">Word Clock</h2>
<p>Before we get started, here's what I built!</p>

<p align="center">
<!-- <embed width="800" height="500"
src="https://www.youtube.com/v/60GAwAqii0k"> -->
insert youtube video here
</p>

<h2 class="section-heading">What is it?</h2>
<p>
</p>

<h2 class="section-heading">Materials</h2>
* 1000uf capacitor
* RGB LED Strip - Addressable
* Arduino Uno
* Michaels Shadowbox
* Foam Core Board
* Real Time Clock Module
* Access to printer bigger than 8.5x11

<h2 class="section-heading">The Code</h2>


<p>This code is pretty simple, all I do is take in input from the potentiometer which is set as init. I then scale that value to work with rgb values by dividing by four which is the variable potValue.  After that, I set the color of the strip using a for loop and differing values depending on the potentiometer value.</p>



<h2 class="section-heading">The Circuit</h2>
<img src="http://i.imgur.com/i0ejj5r.jpg" >
<p>This circuit is pretty simple as well! All I have are two main components: the LED RGB Strip and the Potentiometer. Just connect each one to ground and power and then for the LED strip connect the data portion to one of the Input pins designed for PWM. For the potentiometer connect the remaining data portion to analog in to read data from the potentiometer. After you have that, you're pretty much all set. You now have a working mood light if you did everything correctly!</p>

<h2 class="section-heading">Credit where credit is due:</h2>
