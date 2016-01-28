---
layout: page
title: "7. Communicating through Events"
---

The Particle Cloud let's us do lots of awesome things like put functions and variables from our microcontroller online quickly through a REST API. It also let's us pass useful messages to devices that are interested in hearing what our microcontroller's got to say. It does this through it's events. Event's a mini messages, you can share them from your device or from anything with access to the Cloud API, and you can listen for them. As you share (or publish an event), those devices that are listening are notified and can do stuff with the information.

In this section we'll explore events as a great way to pass information between internet appliances and nudge them to do cool stuff with it. 


### Some background

* Guide: [Particle Cloud and Events]({{site.baseurl}}/7-communicating-events/events)

### Two worked examples

1. Tutorial: [A PIR and Particle.publish()]({{site.baseurl}}/7-communicating-events/pir)
1. Tutorial: [Events between devices - creating a connected doorbell]({{site.baseurl}}/7-communicating-events/doorbell)


