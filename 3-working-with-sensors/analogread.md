---
layout: page
title: "Reading from Sensors: Using analogRead"
---



Up until now, we’ve only controlled the flow of power to our components. We’ve used <code>digitalWrite</code> to turn power on and off to a pin and <code>analogWrite</code> to perform PWM operations and modulate the power to our components to simulate a lower voltage when fading LEDs.

Remember that sensors transform physical properties of the world into electricity. This means that we need a way to find out how much voltage is being given off by a sensor to find out what it is they are sensing. In order words, we don’t want to write to them, we want to be able to **read** from them

Thankfully, microcontrollers and Arduino let us do just this. 

<code>analogRead</code> is the method that let’s us read the voltage being sent to a pin. To use this method we need to use the analog pins on our Spark microcontroller. They’re labelled from <code>A0</code> to <code>A7</code> on side of the board.

When we connect a sensor to the analog pins, we can use the <code>analogRead</code> read method to see how much voltage is passing to the pin. The <code>analogRead</code> will then return us an integer value between 0 and 4095 (4096 increments) which tells us what the sensor is sensing!

{% include note.html type="warning" title="A little different from Arduino" text="If you’ve used Arduino before, this looks a little different. In Arduino microcontrollers, the range is between 0 and 1023 (1024 increments). If you use Arduino examples make sure to account for this!" %}


Imagine you have a sensor, let’s say a light sensor. We’ll put it on analog pin 0. This is roughly what we need to do: 

````
int lightSensorPin = A0; // connected to analog pin 0

void setup()
{
    // We don’t need to do anything here. 
}

void loop()
{
  int val = analogRead(lightSensorPin); // read from the sensor
}
````

If things are really bright, we’d expect the value we get to be really high - nearer 4095

If things are really dim, we’d expect a low value - 100 or less. 


## Note on Digital Pins

You can use the analog pins as digital pins to control LEDs and to do output. For example, we can use digitalWrite on <code>A0</code>, <code>A1</code> or <code>A7</code> to control an LED. You just need to say that the pin is being used for <code>digitalWrite</code> actions in the setup with <code>pinMode()</code>

## Note on <code>pinMode()</code>

You might have expected to see pinMode called to set the pin to INPUT in the setup. We don’t need to do this for pins being used with <code>analogRead</code>. For two reasons:

1. when <code>analogRead()</code> is called is sets the analog pin for input automatically.

2. <code>pinMode()</code> is used to configure digital pins, and isn’t used for analog pins

## Find out more

* [https://docs.particle.io/reference/firmware/photon/#analogread-adc-](https://docs.particle.io/reference/firmware/photon/#analogread-adc-)
* [http://arduino.cc/en/Reference/AnalogRead](http://arduino.cc/en/Reference/AnalogRead)

