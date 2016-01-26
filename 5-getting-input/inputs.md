---
layout: page
title: "Inputs: Making Physical Interfaces "
---

{% include figure.html src="../images/input/image_0.jpg" caption="" class="" %}

We looked at sensors which allow us to translate physical conditions of the world into electrical stimulus. Now we’ll look at how we can use "inputs" from button presses, sliders, and things like that.

Input devices work much like sensors and we use the same way of finding out what state they are in. They work in two major types: switches and push buttons which will always either be on or off i.e. we want to use digitalRead to know if power is flowing (HIGH) or if it isn’t. Some inputs like potentiometers and sliders work like FSRs or photocells. They are variable resistors that instead of environmental properties, use human action to change how much resistance they apply to our circuit. These inputs give us values in a range. 

## Types of Sensors

Inputs come in all shapes and sizes. Take a look at Sparkfun or Adafruit to see the variety of buttons, switches, sliders, push buttons and more you can use in your projects

* [http://www.adafruit.com/categories/235](http://www.adafruit.com/categories/235) 

* [https://www.sparkfun.com/categories/145](https://www.sparkfun.com/categories/145) 

## Input Components in your Kit

In your Maker kit you have a bunch of input components included. These are:


{% include figure.html src="../images/input/image_1.jpg" caption="A mini push-button" class="small right" %}

#### Mini Pushbuttons

These are nifty little switches that plug nicely into a breadboard or a proto-board. They are normally-open type and are rated at 12V, 50mA.

Know that push-buttons are momentary switches - when you push them they pop right back up - and they come in all shapes and sizes to suit your project!

{% include figure.html src="../images/input/image_2.png" caption="DPDT Switch " class="small right" %}

#### DPDT Switch 

This is a tiny Double Pole Double Throw (DPDT) Switch with 6 legs.

Like Pushbuttons you can find switches in all shapes and sizes. They all work the same - just bigger/smaller/just right.

{% include figure.html src="../images/input/image_3.jpg" caption="Rotary Potentiometer" class="small right" %}

#### Rotary Potentiometer

This is a variable [resistor]({{site.baseurl}}/1-a-simple-internet-appliance/resistors) whose value can be changed by simply turning the knob. 



