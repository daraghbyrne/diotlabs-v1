---
layout: page
title: "A PIR and Particle.publish()"
---

{% include figure.html src="../images/pir_0.png" caption="" class="" %}


PIR’s or Pyroelectric/Passive InfraRed Sensors allow you to detect motion. They detect infrared radiation (given off as heat from humans for example) to find out if a person or other living thing is within the range of the sensor.  They’re what are used in most home security systems to detect motion and intruders. 

They’re low cost and reasonably easy to use, but more complicated than the sensors we’ve worked with before. 

You can read more about them here: [https://learn.adafruit.com/pir-passive-infrared-proximity-motion-sensor/overview](https://learn.adafruit.com/pir-passive-infrared-proximity-motion-sensor/overview)

## Using a PIR

We’re going to create a simple motion detector that will publish an event when someone moves in front of it. 

You will need

* Particle Microcontroller 

* [Breadboard]({{site.baseurl}}/1-a-simple-internet-appliance/breadboards)

* [Jumper Wires]({{site.baseurl}}/1-a-simple-internet-appliance/jumpers)

* A 1k[Ω](http://en.wikipedia.org/wiki/Omega) [Resistor]({{site.baseurl}}/1-a-simple-internet-appliance/resistors)

* A [LED]({{site.baseurl}}/1-a-simple-internet-appliance/leds)

* A PIR sensor

## Step 1: Wiring the PIR

It has three pins, that need to be wired specifically. Wire the + or RED wire to power, wire the black or terminal marked - to Ground and wire (normally the middle) terminal to a digital Pin which we’ll use to read from. 

PIR’s will tell us if motion is detected or not, by allowing power to flow or turning it off. They give us a binary (two options) signal - HIGH or LOW. This is why we wire them to the digital pins.

The circuit, wiring and components are as follows:

{% include figure.html src="../images/pir_1.png" caption="" class="" %}


## Step 2: Setting up the Sketch 

````
int inputPin = D0;              // choose the input pin (for PIR sensor)
int ledPin = D1;                // LED Pin
int pirState = LOW;             // we start, assuming no motion detected
int val = 0;                    // variable for reading the pin status

int calibrateTime = 10000;      // wait for the thingy to calibrate

void setup()
{
  pinMode( ledPin, OUTPUT );
  pinMode(inputPin, INPUT);     // declare sensor as input
}

void loop()
{

  // if the sensor is calibrated
  if ( calibrated() )
  {
  // get the data from the sensor
    readTheSensor();

    // report it out, if the state has changed
    reportTheData();
  }
}

void readTheSensor() {
  val = digitalRead(inputPin);
}

bool calibrated() {
  return millis() - calibrateTime > 0;
}

void reportTheData() {

  // if the sensor reads high
  // or there is now motion
  if (val == HIGH) {

    // the current state is no motion
    // i.e. it's just changed
    // announce this change by publishing an eent
    if (pirState == LOW) {
      // we have just turned on
      Particle.publish("designingiot/s15/motion");
      // Update the current state
      pirState = HIGH;
      setLED( pirState );
    }
  } else {
    if (pirState == HIGH) {
      // we have just turned of
      // Update the current state
      pirState = LOW;
      setLED( pirState );
    }
  }
}

void setLED( int state )
{
  digitalWrite( ledPin, state );
}

````


## Step 4: Compiling and sending to your Particle

Compile and move about!


## Step 5: Check the Event

If you’re on  Mac OSX, open the terminal and type the following in: 

````
curl 'https://api.particle.io/v1/events/designingiot?access_token=[your_access_token]'
````

You’ll see a list of the events being published!

## Find out more 

* [https://learn.adafruit.com/pir-passive-infrared-proximity-motion-sensor/using-a-pir](https://learn.adafruit.com/pir-passive-infrared-proximity-motion-sensor/using-a-pir) 

* [https://gist.github.com/zsup/9496462](https://gist.github.com/zsup/9496462) 

