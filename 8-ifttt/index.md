---
layout: page
title: "8. Connecting to Services with IFTTT"
---

The Particle Cloud is great for 'rolling your own' IoT API's, but there's hundreds if not thousands of things that don't involve Particle that we might want to be able to connect to. We might want to: 

* Send an email from our board
* Deliver a push notification to your mobile device
* Send a tweet to our followers 
* Post to Slack
* Send a SMS to a friend
* Look up or respond to changes in the weather
* Monitor a variable and store it to Google Drive
* Do something when your phone take a new photo
* Interact with other consumer products like set the temperature on your Nest thermostat, change the color of your Hue Lightbulbs or get alerted when someone activates one of your Belkin Smart Sockets.
* __and the list goes on...__


## Enter IFTTT

This is exactly what [IFTTT](https://ifttt.com) or IF THIS THEN THAT let's us do. It's figured out the hard parts of working with online services, other products and other people's APIs. It makes them easy to connect to through quick 'recipes' which do this when that happens. You set what your trigger is (a variable on your board changes to something new or your thermostat changes temperature) and then it takes action (sends an email, shares a link, etc.). 

Just set up an account, connect the [Particle channel](https://ifttt.com/particle), and then create your first recipe. Once you've done that... point it at your Particle. 

## Trigger + Action = Recipe

Within the Particle channel on IFTTT you get lots of ways to interact with your board. These are:

__Triggers:__

* New event published - trigger an IFTTT action when you publish an event from your board
* Monitor a variable - fires when a value on your Particle device changes to something interesting. 
* Monitor a function result - checks a function on your device to see if something interesting is happening.
* Monitor your device status -  fires when your device changes states (i.e. when it goes online or offline.) - useful to know if the power is out or if something's gone wrong!

__Actions:__

* Publish an event - publishes an event back to your device(s), which you can catch with particle.subscribe.
* Call a function - calls a function on one of your Devices, triggering an action in the physical world.
	

### Online resources

* [Particle and IFTTT](https://www.particle.io/ifttt)
* [About IFTTT](https://ifttt.com/wtf)
* [Particle Channel on IFTTT](https://docs.particle.io/guide/tools-and-features/ifttt/)
* [Beginner Tutorial: IFTTT - Monitor a Device Status Trigger](https://community.particle.io/t/beginner-tutorial-ifttt-monitor-a-device-status-trigger/9406?redirected=true)

**Example Recipes for the IOT**

* [https://ifttt.com/recipes/collections/32-recipes-for-the-internet-of-things](https://ifttt.com/recipes/collections/32-recipes-for-the-internet-of-things)