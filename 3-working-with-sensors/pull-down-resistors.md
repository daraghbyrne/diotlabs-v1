---
layout: page
title: "Resistive Sensors and Pull Down Resistors"
---

Pull down resistors are often used with sensors, especially with resistive sensors like the Photoresistor (light sensor) and Force Sensitive Resistor (FSR). An easy way to normally spot a resistive sensor is that it will have two terminals (legs) instead of three. 

Three terminal sensors typically have a power, ground and sensor reading terminal. However, a two terminal (resistive) sensor has electricity (voltage) flow through the component, as a result of the sensing elements, the current is impeded. *For example* in the case of the photoresistor, when bright light is hitting the component, the current will flow unimpeded and the sensor will read a high value. When there is little light hitting the component, the current will be resisted and you will get a low value. 

The problem is we still need a complete circuit (where everything can flow to ground) and the ability to read the sensor reliably. 

We do this with a Pull-Down Resistor: This is where one terminal is connected to the Power (3V3) and the other to a resistor which connects to **ground**. The terminal which connects to the resistor also connects to the analogPin. That gives us a complete circuit where the current flows to ground but it is safely and cleanly connected to the analogPin.

The resistor that we use is important. We must use a high resistance. We want a **10k[Ω](http://en.wikipedia.org/wiki/Omega)** [Resistor]({{site.baseurl}}/1-a-simple-internet-appliance/resistors) - **10KΩ:** BROWN, BLACK, **ORANGE**, [GOLD]


{% include note.html type="warning" title="Spot the Difference" text="There is very little difference visually between a 1K and 10K resistor. <br/><br/>Make sure you use the right one. <br/><br/>A 1K resistor is brown, black, RED while a 10K resistor is brown black ORANGE." %}

## Why do we do this?

Pull-down resistors are used to establish a ‘known output impedance’ or in other words give us a signal that we can reliably read from. It helps to reduce noisy and erratic readings in the sensor signal which results from the way resistive sensors work. 

There’s a little bit of math behind this which uses Ohm’s law (see earlier)

You can read a more detailed explanation below. 

# Find out more:

* [http://playground.arduino.cc/CommonTopics/PullUpDownResistor](http://playground.arduino.cc/CommonTopics/PullUpDownResistor)

* [http://makezine.com/2009/03/05/understanding-pullup-and-pulldown-r/](http://makezine.com/2009/03/05/understanding-pullup-and-pulldown-r/)

* [http://electronics.stackexchange.com/questions/70009/why-use-a-pull-down-resistor-with-a-ldr-and-microcontroller](http://electronics.stackexchange.com/questions/70009/why-use-a-pull-down-resistor-with-a-ldr-and-microcontroller)

* [https://learn.adafruit.com/photocells/using-a-photocell](https://learn.adafruit.com/photocells/using-a-photocell)

