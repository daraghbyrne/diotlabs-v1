---
layout: page
title: "Extending Functionality: Libraries"
---

We saw earlier that we can write functions to wrap a bunch of related operations and make them available as a single method or function call. This is really handy for when we want to use the same actions or operations repeatedly in different places of our code or make that functionality available on the web. Sometimes though a function isn’t enough to make it easy to access repeated functions. 

We’ll take a look at something called Libraries… and use one to control the RGB Led on the Particle board

## What is a Library and why use it?

You’ve already used a few libraries but we haven’t called attention to it. For example the cloud functions for Particle use a library called ‘Particle’, that’s why we call these functions like <code>Particle.function</code> or <code>Particle.variable</code>. In week 1, we also used the WiFi library to find your Particle device’s MAC address so we could connect it to the CMU network

Libraries extend the basic functionality of the Arduino language and the capabilities of the Particle platform. Broadly, you can think of a library as a set of related functions grouped together. A library groups actions for a specific purpose together and makes it much easier to perform those actions. 

They encapsulate, or hide, all of the operations that are performed and simply provide you with a well organized way to do the things you want. 

## What are Libraries used for and what libraries are available?

All sorts of things. They offer extra stuff to help you use and control specific components like motors, LEDs, connecting to WiFi, connecting to services online, communicating with other devices and more!

Particle comes with some built in libraries that you can find full descriptions of at [http://docs.particle.io/firmware/](http://docs.particle.io/firmware/) These include:

* Particle - cloud functions

* WiFi - connecting and communicating with WiFi networks

* SPI - for communicating with SPI devices 

* UDP - for UDP messaging

* Servo - for controlling servo motors

* RGB - for controlling the built in RGB light on the board

* Time - for managing the time functions and calls

There is also a lot of user contributed libraries where people in the Particle community have extended the functionality and made it available for anyone to use.  Visit: [http://particle.io/build](http://particle.io/build) and click to the Libraries option to see the full list

{% include figure.html src="../images/build-libraries.jpg" caption="Example of some of the community contributed libraries available for Particle (see [Particle Build](http://particle.io/build) for a full list)" class="" %}


## Using Libraries

Using Libraries works a little differently depending on where you're writing your code.

#### If you're using the online Particle Build...

You can include a library in an application by opening the library drawer, finding a library that will work for your project, and clicking the "include in app" button. This will add an #include statement to your code that will expose all the capabilities of the library to your code.

#### If you're using the desktop Particle Dev...

1. Find the Library that you want to include (by searching through the online build or searching GitHub). 
2. Download the repository to your Desktop 
3. There'll be a folder called 'firmware'. Find it and copy all of the .cpp and .h files to your project folder.
4. Finally, include your library by adding the following code to the top of your project file 
	
````
#include "LIBRARY.h"
````

You can also find these steps on [the Particle documentation](https://docs.particle.io/guide/tools-and-features/dev/#using-community-libraries). 

## Advanced: Converting Libraries

The Particle community is really active and has "ported" [hundreds of Libraries for Arduino](http://community.particle.io/t/libraries-to-update-for-the-photon/12000) (i.e. converted so that it'll work with). 

If you come across a library that you'd really like to use in your Particle project but it's not yet ported, you can [follow this guide to move it over](https://github.com/harrisonhjones/Spark-Ported-Libraries) - it's a little involved but not too complicated. 

That said, make sure you've checked the forums first. Likihood is you're not the first person to look for the library; and someone's already done the work for you. Make sure you google it and save some time and heartache!


## Find out more:

* [Using Community Libraries with Particle Dev](https://docs.particle.io/guide/tools-and-features/dev/#using-community-libraries)

* [Latest Libraries for Particle](https://community.particle.io/c/libraries)

[http://arduino.cc/en/Reference/Libraries](http://arduino.cc/en/Reference/Libraries)

[https://learn.adafruit.com/adafruit-all-about-arduino-libraries-install-use/arduino-libraries](https://learn.adafruit.com/adafruit-all-about-arduino-libraries-install-use/arduino-libraries)

