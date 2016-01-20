---
layout: page
title: "Understanding your Particle Photon"
---
Shamelessly copied from [http://docs.particle.io](http://docs.particle.io) 

{% include figure.html src="../images/Photon-Matchbox.jpg" caption="The Particle Photon (credit: [Analysir] (http://www.analysir.com/blog/2015/06/16/porting-analysir-firmware-to-particles-photon-platform/))" %}

# What is a Particle Photon?

The Particle Photon is a Wi-Fi development kit for internet-connected hardware. It is, in essence, the "brains" of a connected hardware product or project.

The Photon has on board a microcontroller, which is a small, low-cost, low-power computer that can run a single application. The microcontroller runs the show; it runs your software and tells the rest of the Photon what to do.

Microcontrollers are particularly good at controlling things; hence the name. They have a set of "pins" (little spider leg type things sticking off the chip) that are called GPIO (General Purpose Input and Output) pins, or I/O pins. They can be hooked to sensors or buttons to listen to the world, or they can be hooked to lights and motors to act upon the world. These microcontroller's pins have been directly connected to the headers on the sides of the Photon so you can easily access them; specifically, the pins labeled D0 to D7 and A0 to A7 are hooked directly to the microcontroller's GPIO pins.

The microcontroller can also communicate with other chips using common protocols like Serial (also called UART), SPI, or I2C (also called Wire). You can then make the Photon more powerful by connecting it to special-purpose chips like motor drivers or shift registers. Sometimes we'll wrap up these chips on a Shield, an accessory to the Photon that makes it easy to extend the Photon.

The Photon also has a Wi-Fi module, which connects it to your local Wi-Fi network in the same way that your computer or smartphone might connect to a Wi-Fi network. The Photon is programmed to stay connected to the internet by default, so long as it can find and connect to a network.

When the Photon connects to the internet, it establishes a connection to the Particle Cloud. By connecting to the Cloud, the Photon becomes accessible from anywhere through a simple REST API. This API is designed to make it very easy to interface with the Photon through a web app or mobile app in a secure, private way, so that only you and those you trust can access the Photon.

{% include figure.html src="../images/spark3-900x700.jpg" caption="The Particle Photon (credit: https://www.fabtolab.com/spark-photon-wifi-module)" %}

# What do the Buttons do?

There are two buttons on the Photon: the **RESET** button (when holding the Photon with its USB-port to the top, it's the button on the right) and the **MODE** button (on the left).

The RESET button will put the Photon in a hard reset, effectively depowering and repowering the microcontroller. This is a good way to restart the application that you've downloaded onto the Photon.

The MODE button serves three functions:

* Hold down the MODE button for **three seconds** to put the Photon into **Smart Config **mode to connect it to your local Wi-Fi network. The LED should start flashing blue.

* Hold down the MODE button for **ten seconds **to clear the Photon memory of Wi-Fi networks.

* Hold down the MODE button,** tap once on the RESET button and wait for ten seconds** to do a **Factory Reset**, where the Photon is reprogrammed with the software that was installed on the Photon in the factory. The LED should turn white for three seconds and begin flashing quickly; when the LED switches to another color the Photon has been reset. This is useful if you encounter bugs with your firmware, or if you just want to get back to Tinker.

{% include figure.html src="../images/photon_diagram.png" caption="Diagram of the Photon board and it's pins and buttons! (credit: [Particle](https://docs.particle.io/datasheets/photon-datasheet/))" %}


# What do the LEDs (Light Emitting Diodes - or lights) tell me?

There are two LEDs on the Photon. The big fat one in the middle is a full-color RGB LED that shows you the status of the Photon internet connection. The other small blue LED is the user LED; it's hooked up to D7, so when you turn the D7 pin HIGH or LOW, it turns on and off, respectively.

The RGB LED could show the following states:

* **Flashing blue**: Listening mode, waiting for network information.

* **Solid blue**: Smart Config complete, network information found.

* **Flashing green**: Connecting to local Wi-Fi network.

* **Flashing cyan**: Connecting to Particle Cloud.

* **High-speed flashing cyan**: Particle Cloud handshake.

* **Slow breathing cyan**: Successfully connected to Particle Cloud.

* **Flashing yellow**: Bootloader mode, waiting for new code via USB or JTAG.

* **White pulse**: Start-up, the Photon was powered on or reset.

* **Flashing white**: Factory Reset initiated.

* Solid white: Factory Reset complete; rebooting.

* **Flashing magenta**: Updating firmware.

* **Solid magenta**: May have lost connection to the Particle Cloud. Pressing the Reset (RST) button will attempt the update again.

For an animated illustration of these states see: [https://docs.particle.io/guide/getting-started/modes/photon/](https://docs.particle.io/guide/getting-started/modes/photon/)


The RGB LED can also let you know if there were errors in establishing an internet connection. **A red LED** means an error has occurred. These errors might include:

1. **Two red flashes**: Connection failure due to bad internet connection. Check your network connection.

2. **Three red flashes**: The Cloud is inaccessible, but the internet connection is fine. Check our [Twitter feed](http://www.twitter.com/sparkdevices) to see if there have been any reported outages; if not, visit our [support page](https://www.particle.io/support) for help.

3. **Four red flashes**: The Cloud was reached but the secure handshake failed. Visit our [support page](https://www.particle.io/support) for help.

4. **Flashing yellow/red**: Bad credentials for the Particle Cloud. Contact the Particle team ([hello@particle.io](mailto:hello@particle.io)).

# Pins

The Photon has 24 pins that you can connect a circuit to. These pins are:

* VIN: To power the Photon off an unregulated power source with a voltage between 3.6V and 6V, or, if you're powering the Photon over USB, this pin can be used as 5V V~OUT~ to power external components. In this case consider the current limitation imposed by your USB power source (e.g. max. 500mA for standard USB 2.0 ports). Avoid powering the Photon via USB and V~IN~ concurrently.

* 3V3: This pin will output a regulated 3.3V power rail that can be used to power any components outside the Photon. (Also, if you have your own 3.3V regulated power source, you can plug it in here to power the Photon).

* 3V3*: This is a separate low-noise regulated 3.3V power rail designed for analog circuitry that may be susceptible to noise from the digital components. If you're using any sensitive analog sensors, power them from 3V3* instead of from 3V3.

* !RST: You can reset the Photon (same as pressing the RESET button) by connecting this pin to GND.

* GND: These pins are your ground pins.

* D0 to D7: These are the bread and butter of the Particle Photon: 8 GPIO (General Purpose Input/Output) pins. They're labeled "D" because they are "Digital" pins, meaning they can't read the values of analog sensors. Some of these pins have additional peripherals (SPI, JTAG, etc.) available, keep reading to find out more.

* A0 to A7: These pins are 8 more GPIO pins, to bring the total count up to 16. These pins are just like D0 to D7, but they are "Analog" pins, which means they can read the values of analog sensors (technically speaking they have an ADC peripheral). As with the Digital pins, some of these pins have additional peripherals available.

* TX and RX: These pins are for communicating over Serial/UART. TX represents the transmitting pin, and RX represents the receiving pin.


# PWM (Pulse Width Modulation) Pins

When you want to use the analogWrite() function on the Photon, for instance to smoothly dim the brightness of LEDs, you need to use pins that have a timer peripheral. People often call these PWM pins, since what they do is called Pulse Width Modulation. The Photon has 8 PWM pins: A0, A1, A4, A5, A6, A7, D0 and D1.


{% include figure.html src="../images/ParticlePhotonPin.png" caption="Pin Mapping and Associated Features (credit: [Viper](http://doc.viperize.it/board.viper.particle_photon/r0.3.0/))" %}