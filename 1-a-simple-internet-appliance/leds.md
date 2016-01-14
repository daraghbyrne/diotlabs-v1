---
layout: page
title: "Understanding LEDs (aka Light Emitting Diodes)"
---

{% include figure.html src="../images/image03.gif" caption="Lots of little lights" class="" %}

LED’s come in a variety of shapes, sizes and colors, but they all do one thing: emit light. 

When electricity is passed through the component, it releases this energy as light in a process called electroluminescence. 

While LED’s have two leads or wires like a resistor and other components, they do have a distinction: they are directional. Components that work only in 'one direction' are called **Diodes.** 

You’ll notice that one of the legs is shorter than the other and this is important. The longer leg is called the **anode** (positive). The shorter leg is called the cathode (negative). The anode needs to connect to the power source (positive) while the cathode should be connected to ground (negative). Because of this we need to know which leg is which.

{% include figure.html src="../images/image00.jpg" caption="Know which end of an LED is which" class="" %}

# Brightness

LED’s come with different levels of brightness and in two main types. The level of brightness is indicated by the mini-candala scale where 10 would be dim, 5000 would be bright, and 50,000 is ultrabright. LEDs can also be **clear** or **diffused** and this affects how the light is seen. The light from a clear LED is often directed and powerful while diffused have a softer glow and can be seen from almost any angle. Think of a clear LED as a torch shining light in a specific direction while diffuse would be more like a brake light on a car. 

Brightness can be changed in a few ways. You can add different resistor before the LED to impede the voltage to it or you can connect it to different voltages directly (9V power would shine brighter than 5V which would be brighter than 3.3V power). We can also change the brightness programmatically with a trick called Pulse Width Modulation. We’ll explore this later. 

# What, No light?!?!

Remember that the LED is directional and that the anode (longer leg) should go towards the positive voltage. LED’s that are backwards don’t work, but they don’t get damaged either.

If your LED won’t light up, try turning it around. Even if you had it in the right way, you won’t do it any harm by changing it around. 

# Learn More:

* AdaFruit has a great write up on everything LED - [https://learn.adafruit.com/all-about-leds](https://learn.adafruit.com/all-about-leds)

