---
layout: page
title: "Movement and Motors"
---

{% include figure.html src="../images/output-motors.jpg" caption="" class="" %}


Motors allow us to add movement to our devices. By controlling the flow of power to them we can adjust how they move (the speed, direction and a bunch of other things). 

There are three main types of motor and they each work a little differently.

* **DC Motors (bottom left):** Spin continuously. The only component of movement that you can control is the speed. We use [PWM]({{site.baseurl}}/2-leds-continued/pwm) to adjust the speed of movement and wire to a PWM pin

* **Servos (upper left):** Servos motors can be positioned exactly. We can tell the stepper where we want it to move to. Typically we use a *Library* to hide all the complexity of these operations, and the library will let you choose a range in angles to set the position of the servo. This is normally from 0 to 180 degrees

* **Steppers (upper right)**: Servos are moved in increments. Fluctuations the power sends a signal to the motor to move a tiny amount. You can’t position it exactly (i.e. move to 173 degrees) but unlike servos you can continuously rotate a stepper (go around and around). Some steppers can move backwards and forwards. 

Motors come in various shapes and sizes. Some motors will require higher power but they can do more - they have more torque (or can apply more force) to lift heavy objects etc. When using motors be sure to check the power requirements. 

## In your kits

You’ll find a few different motors:

1. A servo - small servo that works well with 3v power supplies is included. 

2. A DC hobby motor - a small low power motor 

3. A vibration motor - a small weighted motor to create vibrations 

## Find out more 

* [https://learn.adafruit.com/adafruit-arduino-lesson-13-dc-motors/overview](https://learn.adafruit.com/adafruit-arduino-lesson-13-dc-motors/overview) 

* [http://playground.arduino.cc/ComponentLib/Servo](http://playground.arduino.cc/ComponentLib/Servo)

* [http://arduino.cc/en/reference/servo](http://arduino.cc/en/reference/servo)

* [http://arduino.cc/en/Tutorial/sweep](http://arduino.cc/en/Tutorial/sweep)

* [https://learn.adafruit.com/all-about-stepper-motors](https://learn.adafruit.com/all-about-stepper-motors)

* [https://learn.adafruit.com/adafruit-arduino-lesson-14-servo-motors](https://learn.adafruit.com/adafruit-arduino-lesson-14-servo-motors)

* [https://learn.adafruit.com/adafruit-arduino-lesson-16-stepper-motors](https://learn.adafruit.com/adafruit-arduino-lesson-16-stepper-motors) 




