---
layout:     post
comments: 	true
title:      "Making Things Move"
subtitle:   "Intro to Motors"
date:       2015-02-09 16:00:00
author:     "Josh Fermin"
header-img: "img/blog/motor.jpg"
---

<h2 class="section-heading">Sensors, Actuators, and Interactions</h2>

<p>Before we got into making things move in our physical computing class, we left off with sensors, actuators and interaction. For my "mini-project" that I created in class, I made a LED that had an on and off switch along with a brightness sensor. I created this using a potentiometer and a simple button. What I was able to build was the following: </p>

<p align="center">
    <img src="{{ site.baseurl }}/img/blog/button.gif" alt="Post Sample Image">
</p>

<small>Description: Demo-ing the button / on-off switch</small>

<p align="center">
    <img src="{{ site.baseurl }}/img/blog/potentiometer.gif" alt="Post Sample Image">
</p>

<small>Description: Demo-ing the potentiometer / brightness</small>

<p>The hardest part about this was actually the button which I thought would have been the easiest, but it turns out that not only was the software side hard to implement, the hardware was hard to implement too. Check out the code below to see why the software was hard to implement:</p>

{% highlight c %}
int buttonPin = 9;
int potPin = A0;
int ledPin = 10;
int lastButtonState = 0;
int buttonPushCounter = 0;

void setup(){
 Serial.begin(9600);
 pinMode(buttonPin, INPUT);
 pinMode(ledPin, OUTPUT);
}

void loop(){
  int buttonValue = digitalRead(buttonPin);
  int potValue = analogRead(potPin);
//  Serial.println(buttonValue);
  
  if (buttonValue != lastButtonState)
  {
    if(buttonValue == HIGH){
      buttonPushCounter++;
    }
  }
  
  lastButtonState = buttonValue;
  
  if (buttonPushCounter % 2 == 0) {
    int val = potValue / 4;
    Serial.println(val);
    analogWrite(ledPin, val);
    delay(potValue);
    digitalWrite(ledPin, LOW);
    delay(potValue);
  } else {
   digitalWrite(ledPin, LOW);
  }
}
{% endhighlight %}


<h2 class="section-heading">Making things Move</h2>

<p>The next half of the class was implementing motors. We learned about 3 different types of motors, but the one we worked with was a servo motor which is used in things that require precise turning. Here is the code I used to implement the server motor, for now it just rotates clockwise 180 degrees and thne back 180 degrees.</p>

{% highlight c %}

#include <Servo.h> 
 
Servo myservo;  
int pos = 0;   
 
void setup() 
{ 
  myservo.attach(9); 
} 
 
void loop() 
{ 
  for(pos = 0; pos <= 180; pos += 1) 
  {                                  
    myservo.write(pos);              
    delay(15);                       
  } 
  for(pos = 180; pos>=0; pos-=1)     
  {                                
    myservo.write(pos);              
    delay(15);                      
  } 
} 

{% endhighlight %}