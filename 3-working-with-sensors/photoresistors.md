---
layout: page
title: "Tutorial: Using a photoresistor"
---

This tutorial will introduce you to the basics of reading values from a photoresistor.

## You will need

* Particle Microcontroller 

* [Breadboard]({{site.baseurl}}/breadboards)

* [Jumper Wires]({{site.baseurl}}/1-a-simple-internet-appliance/jumpers)

* A 1k[Ω](http://en.wikipedia.org/wiki/Omega) [Resistor]({{site.baseurl}}/1-a-simple-internet-appliance/resistors)

* A 10k[Ω](http://en.wikipedia.org/wiki/Omega) [Resistor]({{site.baseurl}}/1-a-simple-internet-appliance/resistors)

* A single color [LED (Light Emitting Diode)]({{site.baseurl}}/1-a-simple-internet-appliance/leds)

* A photoresistor.

{% include figure.html src="../images/photoresistortut_0.jpg" caption="A photoresistor" class="medium right" %}

## Step 1: Identifying your photoresistor

Your photo resistor looks like this. You should have two of them in your Maker kit. A photoresistor is a light sensitive resistive sensor. That means that as light hits the top of the component it varies resistant to electricity. When there is a lot of light, it has a low resistance. When there is dim light, it is highly resistant. 


##  Step 2: Create your Circuit

The circuit, wiring and components are as follows:

{% include figure.html src="../images/photoresistortut_1.png" caption="Fritzing Circuit Diagram" class="" %}
 
Wire up your LED as you did the last time. 

Along your Particle board you will see a series of pins labelled A0 to A7. These are the analog pins which can be used to read from sensors. 

First connect any terminal (leg) of your photoresistor to **A0**. Connect the other terminal to power or the 3V3 Pin. 

We need to include a pull down resistor in order to get accurate readings. Do this by adding a 10K Ohm resistor to the terminal connected to A0. Connect this resistor to ground (GND). 

{% include note.html type="warning" title="Spot the Difference" text="There is very little difference visually between a 1K and 10K resistor.<br/><br/>Make sure you use the right one.<br/><br/>A 1K resistor is brown, black, RED while a 10K resistor is brown black ORANGE." %}

## Step 3: Setting up the Sketch 

Let’s get the basics of our sketch underway.  We are going to combine all of the guides to do the following:

1. read from a sensor,

2. put the sensor reading on the Particle Cloud,

3. map that sensor reading to an output range, and

4. fade the LED to correspond to the sensor reading

If you’d like to get the code for this directly, go to [{{site.github_source_code}}]({{site.github_source_code}})

#### Add your variables

First we want to set a variable for the <code>photoCell</code> and set it to map to A0 (analog pin 0). We also want to create a variable to store any readings that we take from the photo cell. 

We’re going to use D0 again for your LED, so set up a variable that maps to that pin at the top of your sketch. Also add a variable that we’ll use to track the brightness of the LED called <code>ledBrightness</code>; 

````
// Define a pin that we'll place the photo cell on
// Remember to add a 10K Ohm pull-down resistor too.
int photoCellPin = A0;

// Create a variable to hold the light reading
int photoCellReading = 0;

// Define a pin we'll place an LED on
int ledPin = D0;

// Create a variable to store the LED brightness.
int ledBrightness = 0;
````

#### Setup <code>setup()</code>

Now, let’s specify the basics of our sketch. We need to configure pin D0 as output. 

````
void setup()
{
  // Set up the LED for output
  pinMode(ledPin, OUTPUT);
}
````

#### Creating a <code>loop()</code>

In the loop we want to read the current value from the sensor, map that value into a usable range for output and fade the LED to reflect the sensor reading


````
void loop()
{
  // Use analogRead to read the photo cell reading
  // This gives us a value from 0 to 4095
  photoCellReading = analogRead(photoCellPin);

  // Map this value into the PWM range (0-255)
  // and store as the led brightness
  ledBrightness = map(photoCellReading, 0, 4095, 0, 255);

  // fade the LED to the desired brightness
  analogWrite(ledPin, ledBrightness);

  // wait 1/10th of a second and then loop
  delay(100);
}
````

Let’s walk through what is happening here.  The function starts by using <code>analogRead</code> to read from pin A0. This gives us a value from 0-4095 stored in the variable named <code>photoCellReading</code>. 

Next we use this variable and transform it to a range between 0 and 255 based using the <code>map()</code> function. The new value is stored as the <code>ledBrightness</code>.  This is then used to fade the LED and finally the sensing pauses for a moment and repeats. 

#### Connecting to the Cloud

The final piece of the puzzle is to make the light reading available through the Particle Cloud. To do this we add one line to <code>setup()</code> as follows. 

````
void setup()
{
  // Set up the LED for output
  pinMode(ledPin, OUTPUT);

  // Create a cloud variable of type integer
  // called 'light' mapped to photoCellReading
  Particle.variable("light", &photoCellReading, INT);

}
````

This creates a new cloud variable named ‘<code>light</code>’ which is mapped to our existing sketch variable called <code>photoCellReading</code> and says it is an integer (or number).

## Step 4: Compiling and sending to the Particle board.

Make sure the Status Bar has a device connected and the device’s indicator is breathing blue. If not make sure your device is connected by USB and is getting a WiFi signal.

Press the Lightning bolt on the top left of the window. 

You’ll see a message ‘Compiling in the Cloud’ and a few sections later your device should start flashing magenta.

Wait a few moments, it should return to breathing blue, and the LED should be off.

#### Step 5: Seeing your Variable

There’s two ways to control your light. The easy way is through Particle Dev, and then you can make a RESTful API call. We’ll do both.

#### Using Particle Dev.

Select the Particle menubar item, and choose the ‘Show Cloud Variable’ option (2nd from the bottom) and the following screen will appear and display and variables you registered. 

Click the Watch button to have it refresh every few seconds.

{% include figure.html src="../images/photoresistortut_2.jpg" caption="Seeing the cloud variable" class="" %}

#### Using the REST API

* Open up [http://particle.io/build](http://particle.io/build)

* Select the Target Icon to view your devices. Select the device which is currently connected and the device ID information will appear.

* Copy down the device ID - you’ll need that in a second.

* You also need an Access Token. To get that click on the ‘Settings’ icon. You’ll see an access token string. Copy this down too.

* Modify the below and paste it into a Terminal Window

````
curl https://api.particle.io/v1/devices/[deviceID]/light?access_token=[token]
````
		

You will get a response like

````
"cmd": "VarReturn",
  "name": "light",
  "result": 125,
  "coreInfo": {
    "last_app": "",
    "last_heard": "2015-01-21T02:25:55.359Z",
    "connected": true,
    "deviceID": "53ff70066667574826292067"
  }
````

#### Using the CLI

If you have the command line interface installed on your desktop you can access Particle variables as follows

Simple call the following (and replace the square brackets with your actual device ID!): 
`````
particle variable get [device_id] light
`````


#### Using the Provided WebPage

Open up the webpage and enter your Device ID and Access Token for Particle cloud. It uses JQuery to make calls directly to the cloud API and your variable available in the browser.

#### Additional Exercises

Get some practice in! 

{% include note.html type="tip" title="Exercise 1" text="Currently the program shows how much light is available. When there is lots of light the LED is bright. When there is little light it’s dim.<br /><br />Modify the program so that the LED shows the opposite. When there is little light, it will be bright and when there’s lots of light, it will be off." %}

---

{% include note.html type="tip" title="Exercise 2" text="Instead of fading your light, why not turn it on or off when the light reaches certain levels. <br /><br />For example, if the light levels are below 600 turn the light on (and bright), otherwise turn it off.<br /><br />Modify the program to work in this way." %}


## Find out more about photoresistors

[https://learn.adafruit.com/photocells/overview](https://learn.adafruit.com/photocells/overview) 

