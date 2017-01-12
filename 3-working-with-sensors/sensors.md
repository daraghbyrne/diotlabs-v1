---
layout: page
title: "What are sensors?"
---


Sensors are a type of component that allow us to find out about the world around us. They tell us about the conditions of the environment or activities taking place from light levels through motion detection to magnetic fields and force.

They convert environmental conditions into electricity which in turn is applied to our circuit and allows the microcontroller to understand what is happening around it. These are known as sensor *readings,***_ _**where we use the microcontroller to read from the component and give a value back. These values are in known ranges, but often different sensors give different ranges back or these ranges mean different things. We need to know a little bit about each sensor in order to *interpret* these sensor readings correctly. We’ll look at how to do this in the next sections and tutorials that come with them.

## Types of Sensors

Sensors are fundamental to physical computing and to the internet of things. They enable all sorts of connected products in the areas of :

* *The Home* - sensors tell us about conditions of the home: noise, light, temperature, or human activity

* The City - sensors can tell us about the conditions of a city as a whole: temperature, barometric pressure, humidity, air quality, gases, dust, etc.

* *Connected Car:* sensors can tell us about location (GPS), activity (acceleration, speed, distance),  proximity (distance/closeness), etc.

* *Connected Health* - here sensors are often called *biometric* sensors or sensors which give readings on the body.

There really are hundreds of different sensors you can use. Three great places to start exploring the variety of sensors available are the Adafruit Store, SparkFun’s Store and Arduino’s article on interfacing with hardware (see section on Input)

* [http://www.adafruit.com/category/35](http://www.adafruit.com/category/35)

* [https://www.sparkfun.com/categories/23?page=all](https://www.sparkfun.com/categories/23?page=all)

* [http://playground.arduino.cc/Main/InterfacingWithHardware#Input](http://playground.arduino.cc/Main/InterfacingWithHardware#Input)

Each sensor is different and converts physical properties of the world into electrical stimulus in very different ways. We need to know a little bit about each type in order to know how to use it.  Thankfully Adafruit and Sparkfun do an excellent job of giving additional documentation for each sensor, and often include basic tutorials too. 

## Sensors in your Kit

In your Maker Kit you have a bunch of sensors included. These are:


{% include figure.html src="../images/temp.jpg" caption="Temperature Sensor" class="small right" %}

#### Temperature Sensor


The DS18B20 is an easy to use one wire digital thermometer with up to 12-bit measurement resolution. It works with low voltage from 3.0V to 5.5V DC. It doesn't need any external calibration and can measure a temperature range of -55°C to +125°C with an accuracy of ±0.5°C (from -10°C to +85°C). It uses the OneWire protocol for digital sensing. 


[comment]: <> The TMP36 is a low voltage, precision centigrade (C) temperature sensor. It provides a voltage output that is linearly proportional to the Celsius (centigrade) temperature. The TMP36 does not require any external calibration to provide typical accuracies of ±1°C at +25°C and ±2°C over the −40°C to +125°C temperature range.


{% include figure.html src="../images/mk-pir.jpg" caption="PIR" class="small right" %}

#### Pyroelectric ("Passive") Infra-Red Sensor

PIR sensors are used to detect motion from people and other living things (like pets) from 1-20 feet away. It tells you if someone has moved in or out of the sensors range. They're often used in home alarm systems and have lots of applications!

{% include figure.html src="../images/photoresistor.jpg" caption="LDRA photo-resistor" class="small right" %}

#### Photo Resistors
LDRA photo-resistor is a light dependent resistor whose resistance decreases with the increase in the intensity of light striking it. You can use it to detect the ambient light in the surrounding, detect shadows or use it as a part of a burglar alarm system.

### Other often used Sensors

Some other useful and often used sensors include: 


{% include figure.html src="../images/tilt.jpg" caption="SW-200D" class="small right" %}

#### Tilt Sensor
SW-200D is a tiny tilt sensor that when tilted to more than 30 degrees will internally connects its two terminals together. The magic happens with the use of gravity and a tiny metal ball. You can use to it detect tilt, orientation or vibrations.

{% include figure.html src="../images/hall.jpg" caption="Hall Effect" class="small right" %}

#### Hall Effect Sensor
This sensor allows you to detect the presence of a magnet. When you hold a magnet near it, the output pin will toggle. It can be used to sense presence or mounted to a door or window can make for a great open/closed sensor. A reed switch can also detect magnets!

{% include figure.html src="../images/fsr.jpg" caption="Force sensitive resistor" class="small right" %}

#### Force-Sensitive Resistor
This is a force sensitive resistor can detect pressure applied to it. They're not terribly reliable and can be difficult to calibrate, but certainly tell if you force is applied and the degree of force. It won't be able to tell you exactly how much force with any confident. Typically they're around a 0.5" diameter and have an operating force from 10g to 1000g - but they also come in all shapes and sizes. Their resistance decreases with an increase in applied pressure.
  
 {% include figure.html src="../images/bend.jpg" caption="Bend/Flex Sensor. Credit: Adafruit" class="small right" %}
 
#### Bend/Flex Sensor
Very similar to the FSR except that it doesn't measure force, it measure the amount of bend. As the sensor is flexed, the resistance across the sensor increases. It's often used in applicantions like smart gloves or wearables to measure how much the body's joints have moved!

{% include figure.html src="../images/thermistor.jpg" caption="thermistor " class="small right" %}

#### Thermistor
A thermistor is a temperature dependent resistor. This one is a NTC type (Negative Temperature Coefficient), which means its resistance decreases with an increase in temperature.


{% include figure.html src="../images/gas-co.jpg" caption="An carbon monoxide gas sensor" class="small right" %}

#### Gas Sensors 

There are a range of sensors calibrated to detect different gases and particles concentrations in the air. Each gas is detected with a distinct sensor and these include carbon monoxide (MQ7), petroleum (LPG - MQ6), hydrogen (MQ8), methane (MQ4), and alcohol (MQ3) to name but a few. There are also dust and air quality sensors that will give you readings on general pollutants and particle concentrations in the air. Great for environmental monitoring! 

#### Accelerometers

Accelerometers allow you to sense acceleration in one or more degrees. 3-axis accelerometers are most often used and let you see acceleration in the x, y, and axes (up, down, left, right, forward and backwards). They can give you information on movement (they're used in game controllers and phones to give input e.g the Wii), shock/impacts (they're used in laptops to detect falls and protect harddrives) and tilt. They're often used in wearables and in things like movable musical instruments. 

There's also gyroscopes to detect velocity, rotation and orientation; and magnetometers which are like digital compasses.


### Find out more... 

There are many, many, many more sensors available in the lab for your projects and you can always order specific sensors from Adafruit or Sparkfun. The [Sensor Pack 900 from Adafruit](http://www.adafruit.com/products/176) or the [SparkFun Sensor Kit](https://www.sparkfun.com/products/12797) are both good starting points!


## Learn more

[Calibrating Sensors on Adafruit](https://learn.adafruit.com/calibrating-sensors)
