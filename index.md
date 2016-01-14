
## Designing for the Internet of Things

#### A Hands on Guide to Programming, Electronics and Building Connected Products

An outline description of tutorials and hands-on self paced guides for this course is described below. 

This guide contains a series of online resources, developed as part of CMU's [Designing for the Internet of Things](http://daraghbyrne.github.io/diot2016//) (24-884). It's designed to offer a series of self-paced guides and tutorials which can be followed during scheduled lab times or at a time of convenience. 

#### Equipment

These guides and labs are designed for use with the [Particle IoT Framework](http://particle.io) and have been updated for the [Particle Photon](https://www.particle.io/prototype#photon) development board. These tutorials assume you are using a [Particle Maker Kit](https://store.particle.io/collections/shields-and-kits) or have access to these components. 

#### Skills building
First, these guides serve as an introduction for those who haven't encountered electronics and programming for microcontrollers before. To help build general skills, these guides cover a range of topics, including (but not limited to):

- Soldering
- Working with electronics, preparing circuits and reading circuit diagrams
- Using an IDE 
- Programming Microcontrollers (coding and development guides for novices)
- Networking and connectivity ( device to device communication, exposing device information and status through APIs, handling events, etc.)
- Sensing, Actuation and Input
- Working with Libraries; and
- Working with advanced components

#### Equipment

These guides and labs are designed for use with the [Particle IoT Framework](http://particle.io) and have been updated for the [Particle Photon](https://www.particle.io/prototype#photon) development board.

These tutorials assume you are using a [Particle Maker Kit](https://store.particle.io/collections/shields-and-kits) or have access to these components. 

#### The Internet of Things and  Organisation of this Material

This material is designed to help students begin to build working prototypes of 'internet appliances'. These are discussed, for example, by McEwen and Cassimally: 

<figure>
	<a href="{{site.baseurl}}/public/images/internet-appliances.jpeg">
		<img src="{{site.baseurl}}/public/images/internet-appliances.jpeg" alt="Source: Designing the Internet of Things by Adrian McEwen & Hakim Cassimally">
	</a>
<figcaption>
	Source: Designing the Internet of Things by Adrian McEwen & Hakim Cassimally
</figcaption>
</figure> 
<br/>

These internet appliances broadly allows a couple of major scenarios to happen:

1. __Putting Data on the Web__: They allow sensors or other components to collect data about the user or the environment the appliance is in and share it on the web. This allows other 'things' to make use of or act on this information. 

2. __Allowing control and access__: They allow us to reach out and change, configure and control our devices from places near and far away. Like for example, using an app to turn on your crock pot or lights before you get home. 

2. __Getting data from the web__: The appliance can access information from services, databases and other things connnected to the web. Often this will be used to either act on the data to configure the home (e.g. local weather used by a smart thermostat to adjusting indoor temperature) or to make useful information visible so that someone can act on it (e.g. an umbrella that lights up if it's going to rain today)

3. __Making thing talk__: Things can talk to other things, either through the data they share or they can directly interface and pass information another device needs or wants. This helps to build an IoT ecosystem where lots of 'internet-enabled appliances' are talking to one another, sharing information and interacting. 

Once we cover the basics of the Particle framework and electronics, we'll look at each one of these through guides, tutorials and examples.


