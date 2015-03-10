---
layout:     post
comments: 	true
title:      "Mood Light"
subtitle:   "RGB LED Desk Lighting"
date:       2015-02-09 16:00:00
author:     "Josh Fermin"
header-img: "img/blog/rgbledstrip.jpg"
---

<h2 class="section-heading">Mood Light</h2>
<p>Before we get started, here's what I built!</p>

<p align="center">
<embed width="800" height="500"
src="https://www.youtube.com/v/60GAwAqii0k">
</p>

<h2 class="section-heading">What is it?</h2>
<p> What I implemented is a RGB LED Strip that would change color based upon the input of the potentiometer. As the potentiometer is turned, the LED strip will react to the value of the potentiometer based upon if statements. 
</p>
<p>When I first got the LED Strip up and running, I instantly had a sweet idea to use it for some back-lighting for my desk. So for this project I simply used some double sided tape and put one long strip on the upper part of my desk. I slapped the LED Strip on there and bam, instant mood lighting!</p>

<h2 class="section-heading">Materials</h2>
* 1000uf capacitor
* Potentiometer
* RGB LED Strip - Addressable
* Arduino Uno
* Double Sided Tape

<h2 class="section-heading">The Code</h2>
{% highlight c %}
#include <Adafruit_NeoPixel.h>
#include <avr/power.h>
#define PIN            6
#define NUMPIXELS      52

Adafruit_NeoPixel pixels = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

int delayval = 500; // delay for half a second
int potPin = A0;

void setup() {
#if defined (__AVR_ATtiny85__)
  if (F_CPU == 16000000) clock_prescale_set(clock_div_1);
#endif
  pixels.begin(); // This initializes the NeoPixel library.
}

void loop() {
  // For a set of NeoPixels the first NeoPixel is 0, second is 1, all the way up to the count of pixels minus one.
  int init = analogRead(potPin);
  int potValue = init / 4;
  setColor(potValue, potValue-255, potValue-127);
}

void setColor(int r, int g, int b) {
    for(int i=0;i<NUMPIXELS;i++){
    // pixels.Color takes RGB values, from 0,0,0 up to 255,255,255
    pixels.setPixelColor(i, pixels.Color(r,g,b)); // Moderately bright green color.
    pixels.show(); // This sends the updated pixel color to the hardware.
  }
}
}
{% endhighlight %}

<p>This code is pretty simple, all I do is take in input from the potentiometer which is set as init. I then scale that value to work with rgb values by dividing by four which is the variable potValue.  After that, I set the color of the strip using a for loop and differing values depending on the potentiometer value.</p>



<h2 class="section-heading">The Circuit</h2>
<img src="http://i.imgur.com/i0ejj5r.jpg" >
<p>This circuit is pretty simple as well! All I have are two main components: the LED RGB Strip and the Potentiometer. Just connect each one to ground and power and then for the LED strip connect the data portion to one of the Input pins designed for PWM. For the potentiometer connect the remaining data portion to analog in to read data from the potentiometer. After you have that, you're pretty much all set. You now have a working mood light if you did everything correctly!</p>