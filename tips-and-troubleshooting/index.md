---
layout: page
title: "Tips and Troubleshooting"
---

We’ll add more as we go.  If you can think of any new additions, please suggest them!

# Problems connecting to Particle

The most common problem will be: *Does your Particle have access to the internet.*

**Solution: Check your Particle board has the right WiFi credentials.**

If you move location for example from campus to home, you need to update the WiFi settings that your Particle board is using to connect to the internet.

1. Connect the Particle board to your computer via the USB cable

2. Open up the ‘Particle Dev’ application

3. Choose the ‘Particle’ Menu and then ‘Setup your Device’s WiFi’

4. Follow the instructions and the Particle device should connect 

------------------------------

For more complex problems… These two guides from the Particle Team are excellent resources. 

* [http://docs.particle.io/troubleshooting/](http://docs.particle.io/troubleshooting/) (especially towards the end)

* [https://community.particle.io/t/spark-core-troubleshooting-guide-spark-team/696](https://community.particle.io/t/spark-core-troubleshooting-guide-spark-team/696)

# Common Stumbling Blocks

------------------------------

**_Problem: My LED won’t light up_**

**Solution: **LED’s have a direction. You’ll see that it has a long leg and a short leg. The long leg is the positive leg and the short is the negative side. Negative should go to ground or GND on your Particle board. 

Remove your LED and check that it is placed correctly. 

------------------------------

**Problem: My circuit isn’t behaving as expected**

**Solution:** There could be a few reasons for this so its helpful to cover a few bases

1. Check your wiring. It could be that you’ve added a connection to the wrong pin accidentally. This is the most common reason.

2. Check your components - see above

3. Check your connections: Do you have any exposed wires? Are they touching off one another? If they are this can cause the current to flow in unexpected ways.

4. Check your code: Maybe its not the components but the code you’re using to control them? Have you correctly mapped to the right Pins? Are you controlling them in the way you expected? 

------------------------------


# Tips for Circuits

* When stripping wires, don’t strip them all the way back. Just expose as much as you need. More exposed wire means more potential for unwanted contact against other components!

* Watch for crossover and contact between wires. This is a common reason for complicated circuits to fail.

* Give as much room as possible for the wires - don't cut short you can always cut short later

* Make sure your circuit is complete - that means that everything flows (and can flow) to ground? [Why does a current need to flow back to ground? - Add link]

