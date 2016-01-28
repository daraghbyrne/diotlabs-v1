---
layout: page
title: "Worked Example: A connected Doorbell!"
---



## What are we going to create

This guide will bring you through the process of creating an internet connected paired device. We’re going to build a simple example which uses a **pushbutton** and a **piezo buzzer** to connect any number of Particle devices together. 

We’ll publish an event that every board will listen to and when it hears it will play a simple melody - on all the devices! 

You will need

* Particle Microcontroller 

* [Breadboard]({{site.baseurl}}/breadboards)

* [Jumper Wires]({{site.baseurl}}/1-a-simple-internet-appliance/jumpers)

* [Piezo]({{site.baseurl}}/5-getting-input/piezo)

* A [push button]({{site.baseurl}}/5-getting-input/buttons)


## Wiring it up 

The circuit, wiring and components should look like this

{% include figure.html src="../images/doorbell.png" caption="" class="" %}


## Setting up the Sketch 

We set up the basics. The pin the speaker and the buttons are on and create a variable to store the state of the button in. 

We also need to create a set of variables to hold the melody when we go to play it back.

````
int speakerPin = A0;

int buttonPin = D0;
int val;

int noteDurations[] = {4,8,8,4,4,4,4,4 };

int melody[] = { 440, 494, 131 };

// note durations: 4 = quarter note, 8 = eighth note, etc.:
int noteDurations[] = { 4,8,8 };
````

Next we setup the sketch so that we can read from the button. Remember we use an internal pullup resistor when dealing with switches. 

````
void setup() {
  
  pinMode( buttonPin , INPUT_PULLUP); // sets pin as input

}
````

In the loop, we’ll want to monitor the button and see if it has been pushed or not.

If it is pressed, we’ll want to trigger an event and let other devices know to play the melody

````
void loop() {
  // read the value from the button pin
  val = digitalRead( buttonPin );

  // if the button is pushed
  if( val == LOW )
  {
      // The doorbell is pushed
      announceDoorbell();

      // Wait for 2.5 seconds before letting
      // another event happen
      delay( 2500 );
  }
}
````



So we know we need a function to announce the doorbell has been pushed. Let’s create that now

````
// Publish an event saying that the
// Doorbell has been pushed
void announceDoorbell()
{
  Particle.publish( "db2015/doorbell-pushed" );
}
````

We use <code>Particle.publish</code> to announce a new event called ‘<code>db2015/doorbell-pushed</code>’. This has a relatively unique name so that it is unlikely other devices will use it. 

##Receiving an event 

Well now we have our board sending out an event when a button is pushed, but we’ll want to listen for new events and respond to them too. 

Let’s modify the setup to let us do that.


````
void setup() {
  
  pinMode( buttonPin , INPUT_PULLUP); // sets pin as input

  // Subscribe to the doorbell event
  Particle.subscribe(  "db2015/doorbell-pushed" , handleDoorbellPush );  
}
````

Ok, so we’ve registered the event, and mapped it to an event handler (function) called ‘handleDoorbellPush’

**Let’s create that event handler now**

````
void handleDoorbellPush(const char *event, const char *data)
{
    doDingDong();

}


void doDingDong()
{
  // iterate over the notes of the melody:
  for (int thisNote = 0; thisNote < 8; thisNote++) {

    // to calculate the note duration, take one second
    // divided by the note type.
    //e.g. quarter note = 1000 / 4, eighth note = 1000/8, etc.
    int noteDuration = 1000/noteDurations[thisNote];
    tone(speakerPin, melody[thisNote],noteDuration);

    // to distinguish the notes, set a minimum time between them.
    // the note's duration + 30% seems to work well:
    int pauseBetweenNotes = noteDuration * 1.30;
    delay(pauseBetweenNotes);
    // stop the tone playing:
    noTone(speakerPin);
  }
}
````

OK

**We have our handler which is immediately going to play the chime. This works as follows:**

* This loops over each note to be played.

* Then it calculates the duration in milliseconds for each note

* It uses the tone function to play that note 

* It pauses for a moment between notes

* Finally it stops playing the note and moves to the next note in the sequence

## One final thing.

**What happens if two doorbells are pushed at once?**

We want to design for this so it doesn’t play crazy. 

It’s a very simple addition to the program. First, let’s add a variable which can keep track of if we’re playing or not.

````
..

// note durations: 4 = quarter note, 8 = eighth note, etc.:
int noteDurations[] = { 4,8,8 };

// Track if the doorbell is playing
boolean isPlaying = false;
````

**Now that we’ve done that… we just modify the event handler a little.**

````
void handleDoorbellPush(const char *event, const char *data)
{
  if( isPlaying == false ){
    // set is playing to true
    isPlaying = true;
    // play the chime
    doDingDong();
  }
  
  // We're done. Allow another chime to play.
  isPlaying = false;

}

````



Now the event handler checks to see if we are playing. If the piezo is already in use, it’s not going to make a second sound or try to interrupt the other. 

## Compiling and sending to your Particle

Ding dong. Compile and try it out! 

{% include note.html type="tip" title="There’s lots of uses for a Piezo" text="An array is a collection of variables that are accessed with an index number.  Read more at: You can use a piezo as a sensor to detect knocks. Read more: [http://www.arduino.cc/en/Tutorial/KnockSensor](http://www.arduino.cc/en/Tutorial/KnockSensor)" %}



