---
layout: page
title: "What is the Particle Platform and what does it do?"
---

[comment]:# What is the Particle Platform and what does it do?


## Origins in Arduino

The Particle platform owes a lot to [Arduino](https://www.arduino.cc/). Arduino is a groundbreaking toolkit which has simplified the creation of interactive devices and programmed circuits. Introduced in 2005, as an inexpensive way for artists, designers, hobbyists, inventors and tinkers to quickly create all sorts of new devices that combine **hardware** and **software**.  

Arduino is incredible, powerful and exciting and it’s led to all kinds of new products and objects. But it does have some limitations: *working with the internet and online services has never been too easy.*

## Designed for IoT

Particle solves that. It’s designed specifically for the internet of things. It allows you to easily combine **hardware**, **software** and the **_internet_** in the Arduino way. It’s makes it quick and easy to share information from your device online and connect interactive devices so they work together. 

If you know Arduino, it will be very familiar to you. If you don’t, because it builds on Arduino  it’ll be easy to learn!

## The Platform

We’ve already mentioned the three majors things that Particle integrates. Let’s talk about them a little more. 

1. **Hardware:** The Particle Photon (and the Core) is a ‘board’ or microcontroller. It’s essentially a small computer with a WiFi connection chip and a small amount of memory to store the software it runs. You’ll see it has a set of ‘legs’ or pins on the underside. These connect up to components, sensors, and circuits to allow you to control them or read information from them. 

2. **Software:** Hardware is hard to change (the clue is in the name), but you can quickly change software to radically adjust how the hardware (and the components it connects to) are used. To make this happen we have to have a couple of things. First, an Integrated Development Environment (IDE) allows you to create programs or ‘sketches’ that the hardware will run. It also has a debugger for checking that the programs are correct, a compiler to convert the program into something the microcontroller can run, and gives you ways to get that ‘sketch’ onto the microcontroller. 

  - Software is written in a simple language that is almost identical to Arduino with just a little extra for internet magic. 

  - To learn the Arduino language visit: [http://arduino.cc/en/Tutorial/HomePage](http://arduino.cc/en/Tutorial/HomePage)

  - To see the Particle language, visit [https://docs.particle.io/reference/firmware/photon/](https://docs.particle.io/reference/firmware/photon/) 

3. **Internet:** The final element - the secret sauce - is the Particle Cloud. This makes it easy to create connected interactive devices. It lets you to make information from your components available online in one line of extra code. It makes it easy to tell other boards and devices about what’s happening and have them respond to it. It makes it easy for you to connect to online applications to get rich real time information about the world or tell the world about what’s happening with your device or in the area around it. 

It presents the information you want to share in an organized way to make it easy for other devices, services, applications to tools to connect to it.  It does this as a structured API or application programming interface. Simply put, an API is a well structured way to access internet data without needing to go through an web page. You can read more at: [https://docs.particle.io/reference/api/](https://docs.particle.io/reference/api/) 

