---
layout: page
title: "Controlling PWM: Using analogWrite"
---

To control LEDs and the flow of power to components we’ve used <code>digitalWrite</code>. This let’s us turn on and off the power by setting the pin to <code>HIGH</code> or <code>LOW</code> as we need. Now that we know we can have more fine grained control over how the power gets to components, we need a function to make that happen. 

<code>analogWrite</code> let’s us perform PWM operations and modulate the power to our components to simulate a lower voltage when fading LEDs.

````
analogWrite(pin, value)

pin: the number of the pin whose value you wish to set
value: the duty cycle: between 0 (always off) and 255 (always on)
````

It works like <code>digitalWrite</code> except that instead of asking for <code>HIGH</code> or <code>LOW</code>, it asks us to tell us how much it should modulate the power on that pin. It asks you to tell it a range from 0 to 255 (or 256 increments), where 0 is the same as LOW and 255 is the same as HIGH or full power. If you said 128 for example, it would modulate the power to 50%. 

__This lets us control the speed of a motor, fade LEDs and control RGB LED’s too.__ We’ll see this in the next set of examples. 


{% include note.html type="tip" title="AnalogWrite + PWM Pins" text="Remember that PWM isn’t available on every pin on your Particle device. The Photon has 9 PWM pins and I'd recommend you stick to D0, D1, D2, D3. A4 and A5 can be used but rememeber that D2/A4 and D3/A5 are paired for PWM operations. If you want to control an LED or a motor using PWM you must have it connected to these pins." %}


## Find out more 

* [https://docs.particle.io/reference/firmware/photon/#analogwrite-](https://docs.particle.io/reference/firmware/photon/#analogwrite-)

* [http://arduino.cc/en/Reference/analogWrite](http://arduino.cc/en/Reference/analogWrite)

