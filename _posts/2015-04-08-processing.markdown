---
layout:     post
comments: 	true
title:      "Processing"
subtitle:   "Hacking Images"
date:       2015-04-01 16:00:00
author:     "Josh Fermin"
header-img: "img/post-bg-11.jpg"
---

<h2 class="section-heading">Etch a Sketch</h2>
<p>For this class we learned how to take serial input from the arduino and transfer it over to processing. This was an extremely valuable lesson for me to learn because I was doing the same thing for my project. So what Jackie taught us was how to create an etch a sketch with the potentiometers in our arudino kits.</p>

<p>All we had to do is download the <a href="http://playground.arduino.cc/interfacing/processing
">Arduino Library for processing</a> and import it into Processing. And then we imported Standard Firmata into Arduino and use the following code in a Processing sketch:</p>

{% highlight c %}
import processing.serial.*;
import cc.arduino.*;

Arduino arduino;
int dial1=0;
int dial2=1;
int x, y, x2, y2;

void setup(){
	arduino = new Arduino(this, Arduino.list()[2], 57600);
	arduino.pinMode(dial1, arduino.INPUT);
	arduino.pinMode(dial2, arduino.INPUT);

	size(600,400); // size of canvas
	stroke(0);

	x=(arduino.analogRead(dial1)*width)/1023; // divide be 1023 to normalize
	y=(arduino.analogRead(dial1)*height)/1023; 
}

void draw(){
	x2=(arduino.analogRead(dial1)*width)/1023; // divide be 1023 to normalize
	y2=(arduino.analogRead(dial1)*height)/1023; 
	line(x,y,x2,y2) // to draw line
	x=x2;
	y=y2;
}


{% endhighlight %}