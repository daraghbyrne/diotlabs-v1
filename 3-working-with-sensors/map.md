---
layout: page
title: "Working with Sensor Data: map()"
---

When working with sensor readings one of the most useful functions the Arduino language offers is map()

Map takes 5 parameters or passed variables as follows:

* value - the name of the variable with the value that you want to transform

* fromLow - the lower bound of the range that the value is currently in 

* fromHigh - the upper bound of the range that the value is currently in 

* toLow - the lower bound of the range that you want to transform the value to

* toHigh - the upper bound of the range that you want to transform the value to

It’s really flexible and great for transforming sensor readings into PWM ranges, or inverting ranges. 

## An example - convert to PWM range

````
int lightSensorPin = A0; // connected to analog pin 0

void loop()
{
  int val = analogRead(lightSensorPin); // read from the sensor

  // analogRead gives us the range 0-4095
  // when we fade an LED we want it in the range 0-255
  // map lets it convert the value like this... 
  int ledValue = map( val, 0, 4095, 0, 255);
}
````


## Another  example - invert a range 

````

int invertedValue = map( val, 0, 4095, 4095, 0);

````

## Another  example - shift a range 

Note that it can also handle negative numbers!

````

int invertedValue = map( val, 0, 100, -50, 50);

````


## Find out more

* [https://docs.particle.io/reference/firmware/photon/#map-](https://docs.particle.io/reference/firmware/photon/#map-)

* [http://arduino.cc/en/reference/map](http://arduino.cc/en/reference/map)

