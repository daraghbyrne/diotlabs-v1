---
layout: page
title: "7. Particle Cloud and Events"
---

Earlier we looked at what the [Particle cloud]({{site.base_url}}/getting-started/the-particle-platform) is and what it does. We’ve also put it to use too with our LED examples where you made [functions of your Microcontroller sketch available]({{site.base_url}}/1-a-simple-internet-appliance/making-functions-available) through the cloud and used it to share data (or variables) from your programs so that anything on the internet can access it. 

The final piece of the puzzle is being able to communicate with other devices in real-time to let them know something important has happened. We want to be able to **announce ‘events’.**

## Important Events

Events are super useful. Instead of just sending out variables and waiting for whatever’s on the other to understand / see that something important has happened, we can explicitly tell another device, a web service or that they should pay attention.

*Imagine we wanted to build a basic security system, we could use a PIR sensor to detect motion and we would want a mobile app to alert you when that happens. To make the alert happen, we could just make the variable available through the cloud, and have the app check it all the time. That’s problematic. It makes it the responsibility of the app to know that it has happened and check a lot. It’s also inefficient as the app will have to make a lot of calls to the API to check it over and over. It’s undirected. The mobile app may not know what it should pay attention to, and it places the burden on the connected device to know the data, make sense of it and interpret it. Really the device collecting the data should do these things.*

Events solve these problems. They let us explicitly say to the mobile app, "hey, I’ve got something you need to know".  And it works both ways, your Particle can look for events it's got to pay attention to too. 

Events are the foundations of device-to-device communication and are what really make the internet appliances possible. 

In order to make events we use the <code>Particle.publish()</code> and in order to listen for events we use <code>Particle.subscribe()</code>. Let’s look at both now in more details

## Thinking of Events: Like twitter for devices

A good way to think of events is to imagine them as Twitter. Think of a network of devices who all want to share what they had for breakfast or how much they like the latest beyonce track playing in the background while they’re at the gym. 

Each device has a ‘feed’ of events - like Twitter - that they can post information to. Other devices can ‘follow’ a device to get updates from them and see what they’re telling the world. 

Some devices might be a little shy so they only let certain people see the information and keep their feed private. 

There’s a little bit more to events, but this is a really good way to think about how it works. 

One major difference from Twitter, is that you can say to a device what information you want to know. You can tell it to only show you selfies or music recommendations! Wouldn’t that be nice to have on Twitter too? 

## Particle.publish()

To publish an event (or tell other things that something important has happened we use this function, but before we say how to use it. Let’s talk a little more about what information an event needs. 

An event needs to know a few things:

* **The name of the event:** The name must be between 1 and 63 ASCII characters (avoid special characters). The name matters. Giving it a recognizable or unique name is important. 

* **Public or private:** Is the event available to everyone on the cloud or only your devices?

* **Time to live (ttl):** How long should the event say active or how long does it live for? By default it says alive for 60 seconds but this can be anywhere from 0-16777215 seconds. This means that other devices can find the event for 60 seconds after it is announced / published.

* **Data:** Not only can you say what’s happening but you can pass some bits of information with the event. You can include a variable or other details that devices looking for this event might find useful.  



{% include note.html type="warning" title="Naming notes" text="You can’t use the word ‘spark’ to begin your events. This is reserved for the Particle cloud to use only." %}



#### Publishing Events

Publishing an event takes one line of code and the only piece of information you really need to give it is the name. All of the other pieces are optional. To send an event we use the syntax:

````
Particle.publish(String eventName);
````

Like this:

````
// EXAMPLE USAGE
Particle.publish("motion-detected");
````


This uses the default information to create an event named ‘motion-detected’ with a ttl of 1 minute which is public. 

We can get more detailed and pass some data like this 

````
Particle.publish(String eventName, char * data);
````

````
// EXAMPLE USAGE
Particle.publish("temperature", "19 F");
// Or
Particle.publish("motion-detected", "Kitchen");
````

This uses the default information to create an event named ‘motion-detected’ with a ttl of 1 minute which is public but it also passes data that might be useful to other devices. 

Let’s add in all of the bits we could use 

````
Particle.publish(const char *eventName, const char *data, int ttl, PRIVATE);

Particle.publish(String eventName, String data, int ttl, PRIVATE);
````

````
// EXAMPLE USAGE
Particle.publish("door-closed", NULL, 30, PUBLIC );
// Or
Particle.publish("motion-detected", "Kitchen", 21600, PRIVATE);
````

The first creates an event called ‘door-closed’, says that there is no information attached and it will be publicly available for 30 seconds.

The second creates an event called ‘motion-detected’, says that it was about the ‘kitchen’ says that it will be available for 6 hours and that it is private or only available to our devices.

{% include note.html type="warning" title="1 a second." text="The Particle API limits the amount of events you can publish from a device. You're only allowed send __1 per second__! Make sure you factor this into your code i.e. add a one second delay! " %}


####  Viewing events

Like function and variable, we can view things that happen on the cloud through an API. 

The API looks like this for all public events (to see all events)

````
GET /v1/events/
````

To see just public events with a specific name, we would do this

````
GET /v1/events/{EVENT_NAME}
````

To see events from a particular device

````
GET /v1/device/{DEVICE_ID}/events/
````

If you’re on a mac. you can use the Terminal to view events as they’re created.

````
curl 'https://api.particle.io/v1/events/?access_token=[access_token]'
````


{% include note.html type="warning" title="Finding events" text="When looking for events, the name works as a partial match. So for example, if you searched for an event named 'motion', it would also return events like 'motion-detected', 'motion-stopped', 'motioned', etc. <br/><br/> It’s important to give your events as specific a name as possible to avoid unexpected conflicts. " %}


## Particle.subscribe()

Now we need to be able to see events when they happen so that the devices can talk to each other. <code>Particle.subscribe</code> allows us to do this easily. 

Using the example from earlier, we can imagine that we have our DIY home security system, and that motion is detected. You could have a second device whose job it is to sound the alarm and let you know when something bad happens. The second device will *subscribe* to listen for events. As soon as a new event that it has subscribed to is published, it will be automatically picked up and it will trigger a specific function (known as an *event handler*) in the program. 

#### Subscribing to Events

To use <code>Particle.subscribe()</code>, you first need to define a handler function and then you register it in <code>setup()</code>.

The handler is like any other function, except that it must take two parameters (or have two pieces of information provided to it always). The first is the event information and the second is the string of data that was passed, like this. You can change <code>‘myHandler’</code> to any name

````
void myHandler(const char *event, const char *data)
````

Next you need to subscribe. You need to tell the subscribe function just two things. First, what is the event name that you want to look for, and next what is the function or handle that will be called when it is found. 

````
Particle.subscribe(String eventName, function);
````
Like this:

````
// EXAMPLE USAGE
Particle.subscribe("temperature", myHandler);
````


This is the way you would listen for public events (which is the easiest), but you can also tell the subscribe function you want to 

1. listen to only private events (from your claimed devices)

2. listen to only events from a specific device

````
// Only from my devices
Particle.subscribe("temperature", myHandler, MY_DEVICES);
// Only from a specific device
Particle.subscribe("temperature", myHandler, "21312312312312312312");
````

Remember that a subscription works like a prefix filter. If you subscribe to "foo", you will receive any event whose name begins with "foo", including "foo", "fool", "foobar", and "food/indian/sweet-curry-beans".


{% include note.html type="warning" title="Subscribe + Private/ Device specific events" text="This is a little tricky and complicated. So my recommendation is to use public events for now. Give your public events a unique prefix so they are specific to you e.g. db2015 etc.<br/><br/>A good name would be <br/>'db2015/motion/detected' or<br/> 'daragh/app25/motion/detected'" %}


{% include note.html type="warning" title="Maximum of Four" text="A Particle device can only subscribe to four events in any one program.<br/><br/>This means you can use Spark.subscribe() a maximum of 4 times in your sketch after that it will not register any new subscriptions." %}


## Read more

* [https://docs.particle.io/reference/firmware/photon/#particle-publish-](https://docs.particle.io/reference/firmware/photon/#particle-publish-)

* [https://docs.particle.io/reference/firmware/photon/#particle-subscribe-](https://docs.particle.io/reference/firmware/photon/#particle-subscribe-)

* [http://blog.particle.io/2014/03/11/spark-publish/](http://blog.spark.io/2014/03/11/spark-publish/)

* [http://community.particle.io/t/spark-publish-for-two-spark-cores/7932](http://community.particle.io/t/spark-publish-for-two-spark-cores/7932)

* [http://www.hackster.io/maxeust/quantumly-entangled-leds1](http://www.hackster.io/maxeust/quantumly-entangled-leds1)

