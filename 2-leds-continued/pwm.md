---
layout: page
title: "Controlling LEDs: All about Pulse Width Modulation"
---

So far we’ve covered the basics of circuits - controlling power to components, making LED’s interactive and writing functions to wrap a set of operations. But turning on and off LED’s is just a little boring, we’d like to be able to do a little more with them, like fading them up and down.  

Before we go on to create an internet connected dimmer switch, let’s find out a little about how we can make it work.

## How it works

We know that resistors can impede the flow of current and reduce the amount of power going to components. Potentiometers are variable resistors (we’ll look at these soon) which allow us to turn a knob and change the amount of resistance. While there are ways to do it, we can’t change the amount of power interactively that a pin will send out.

Thankfully there’s a clever trick we can use to make it seem like the power is varied: we modulate the power. Essentially we’ll turn on and off the power to the pin really really fast (as much as several hundred times a second) and this simulates the conditions of lower power.

Think about someone standing by a light switch and turning it on and off every second. Half the time its incredibly bright. Half the time its dark, but on average its sort of bright. This is essentially what pulse width modulation does. 

It allows us to control the amount of power being sent out by the pin by modulating the amount of power being sent from moment to moment. The diagram below shows how it works. 

{% include figure.html src="../images/pwm.gif" caption="Taken from [http://arduino.cc/en/Tutorial/PWM](http://arduino.cc/en/Tutorial/PWM)" class="" %}


## Pins and PWM

Pulse width modulation is a special function so its not available on every pin on the board. When you want to use the PWM function on your Particle device, you can only use it on certain pins and those are listed below:

* Particle Core boards have 8 PWM pins: A0, A1, A4, A5, A6, A7, D0 and D1.


* Particle Photon boards have 9 PWM pins: D0, D1, D2, D3, A4, A5, WKP, RX, TX. However there's a note: _PWM timer peripheral is duplicated on two pins (A5/D2) and (A4/D3) for 7 total independent PWM outputs. For example: PWM may be used on A5 while D2 is used as a GPIO, or D2 as a PWM while A5 is used as an analog input. However A5 and D2 cannot be used as independently controlled PWM outputs at the same time._ See: [https://docs.particle.io/datasheets/photon-datasheet/](https://docs.particle.io/datasheets/photon-datasheet/#peripherals-and-gpio)

## Find out more:

* [https://learn.adafruit.com/adafruit-arduino-lesson-3-rgb-leds/theory-pwm](https://learn.adafruit.com/adafruit-arduino-lesson-3-rgb-leds/theory-pwm)

* [https://learn.sparkfun.com/tutorials/pulse-width-modulation](https://learn.sparkfun.com/tutorials/pulse-width-modulation)

* [http://arduino.cc/en/Tutorial/PWM](http://arduino.cc/en/Tutorial/PWM) 

* [http://arduino.cc/en/Tutorial/Fade](http://arduino.cc/en/Tutorial/Fade) 

