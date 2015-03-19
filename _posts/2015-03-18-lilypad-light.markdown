---
layout:     post
comments: 	true
title:      "Lilypad and Sewing"
subtitle:   "Learning how to make wearables"
date:       2015-03-18 16:00:00
author:     "Josh Fermin"
header-img: "img/blog/rgbledstrip.jpg"
---

<h2 class="section-heading">Learning How To Sew</h2>
<h3>The Back Stitch</h3>
<img src="http://cdn.shopify.com/s/files/1/0103/0142/files/backstitch_HART.jpg?3996">
<h3>



<h2 class="section-heading">Working with LilyPad</h2>
<p>Before we get started, here's what I built!</p>
<img src="http://i.imgur.com/KEoWHtU.jpg">

<!-- <p align="center">
</p> -->

<h2 class="section-heading">What is it?</h2>
<p> What I implemented a very basic circuit using the lilypad that makes a LED blink on and off. The only difference between this and the arduino is that you can sew your circuit onto material. This allows you to construct wearables as seen from my circuit. I sew the Lilypad circuit and the LED using conductive thread onto a piece of felt. This could have easily been a piece of clothing.
</p>

<h2 class="section-heading">Materials</h2>
<li>Lilypad</li>
<li>LED</li>
<li>Conductive Thread</li>
<li>Felt / Piece of cloth</li>

<h2 class="section-heading">The Code</h2>
{% highlight c %}
void setup() {
  // put your setup code here, to run once:
  pinMode(6, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
  digitalWrite(6, HIGH);
  delay(1000);
  digitalWrite(6, LOW);
  delay(1000);
}
{% endhighlight %}

<p>This code is very trivial, all I did was setup pin 6 (which the LED was connected to by the conductive thread) and then loop it HIGH and LOW with a delay of 1000. This causes the LED to blink on and off.</p>



<h2 class="section-heading">The Circuit</h2>
<img src="http://i.imgur.com/RtP9XRR.jpg">
<p>This circuit is really what makes the difference between Lilypad and Arduino! Instead of plugging in wires I had to use the sewing techniques I learned from class to make this cirucuit connect correctly.</p>