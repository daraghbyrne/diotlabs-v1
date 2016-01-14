---
layout: page
title: "First Sketch: Making an LED Blink"
---

In this exercise, we’re going to create your first circuit, create a short program and control some components with code. You don’t need to know how to program just yet, but there are some additional exercises to help you build those skills at the end. 

### Step 1: Building our Circuit

To make this circuit you need a Particle microcontroller, an LED, a 1K[Ω](http://en.wikipedia.org/wiki/Omega) resistor (brown, black, red) 

Along your Particle device you will see a series of PINs or legs labeled D0 to D7. These are the digitalPins which can be used for input or output. In this case we’ll be using them for output or to turn power on and off to make the LED blink. 

First connect your resistor to **D0** and the other lead to a row on the resistor.

Next add an LED with the anode (longer leg) to the row where the resistor connects. The pin at <code>D0</code> will provide power when it is turned on.

Next we need to connect the cathode to ground. Use your jumper wires to make a connection to the negative column of the power rail (marked in with the blue line) 

Finally, near the GND pin use another jumper cable to connect it to the power rail as shown. Now we have a complete circuit where power from Pin D0 will always flow to ground. 

{% include figure.html src="../images/first-sketch-0.png" caption="Circuit Diagram" class="" %}

This is how your finished circuit should look

{% include figure.html src="../images/first-sketch-1.jpg" caption="Simple Circuit" class="" %}

## Step 2: Getting Ready to Program

Great. We have our circuit ready… now we can use Particle Dev to tell it what to do.

Open up a new Window. Then Save. **Create a new folder called ‘HelloWorld’ and save the sketch inside it as ‘HelloWorld.ino’**



{% include note.html type="warning" title="Why do we need to do this?" text="In order for a sketch to run, it has to be saved in a folder of the same name. Sometimes programs may contain more than one piece of code and have a series of related files or ‘classes’. These are grouped together in the same folder so that when the program is compiled for the microcontroller all the pieces can be easily found. <br/><br/>The main sketch is always the same name as the folder, so the compiler knows where to begin the program.<br/><br/>Finally, we need to include a ‘.ino’ extension on our files so that the development environment recognises them as code to be run on a microcontroller." %}


Your development environment should now look like this:

{% include figure.html src="../images/first-sketch-2.png" caption="Particle Dev" class="" %}

Let’s quickly run through what you see here.

* The **Left hand sidebar** contains a series of icons. These allow you to access common functions quickly

    * Lightning: Compile and deploy your program to your Particle Photon

    * Checkbox: Check your code and find errors.

    * Document: Launch the Particle documentation in your browser

    * Target: Select a device to work with

    * WiFi: Setup a devices WiFi

    * USB: Show serial monitor (useful tool for getting debug information from your Particle when testing sketches)

* The **Document Navigator** shows a list of all the files in your sketch. Double clicking them will open them in the editor

* The **Editor** allows you to create applications that run on your Partile Photon using the Arduino Language. You can have multiple tabs open at once.

* At the bottom of the editor is a **Status Bar**. This contains important information on your sketch, its progress and things that you need to know to successfully get your sketch working. 

    * **Particle Cloud Status**: Displays the status of the particle cloud if you are signed in and lets you know who you are signed in as. If you do not see your user ID, go to the ‘Particle’ menu bar and choose the ‘Sign in’ option

    * **Devices:** In the image above there are ‘No devices selected’ This is bad. In order to get your program working you need to tell the IDE what device (photons) you are working with. Click on the label and you’ll be presented with a list of devices you have associated with your account, then select one!

    * **Language:** On the right hand side you should see a label ‘Particle’. This should almost always say Particle. If it doesn’t check that you have correctly added the  ‘.ino’ extension to your file. 

Step 3: Adding your first program

Now, let’s write some code.

{% include figure.html src="../images/first-sketch-3.png" caption="Coding in the Particle Dev" class="" %}

This is the program that you want to enter in the IDE. You’ll find the code for this example on the GitHub repository or you can feel free to just type it in from below.

Before we do that, let’s explore what’s happening here line by line. 

### Step 3: Defining Variables

The first line of our program is the following. 

````
int ledPin = D0;
````

We have declared a variable of type ‘<code>integer</code>’ and called it ‘<code>ledPin</code>’; that means that the variable called ledPin can only hold a whole number. 

We’ve also assigned this variable a reference to pin <code>D0</code>. Basically, we’ve created a variable we can use to tell other stuff in the program that we want to do things with Digital Pin Zero.

{% include note.html type="warning" title="Global Variables" text="Global variables are defined at the top of the program. Variables which exist outside of curly braces (‘{‘ and ‘}’) are known as global variables because any part of the code can make use of them.<br/><br/>Variables declared inside of curly braces (‘{‘ and ‘}’) can only be used by code which comes after their definition but before the outer curly brace. We’ll look at this again later. " %}


### Step 4: Setting up our sketch

Every sketch needs two functions or blocks of code to exist. The first is <code>setup()</code> and the other is <code>loop()</code>.  Setup is called once every time the program is run. This happens when the program is first put on the microcontroller, every time it is powered on and every time the reset button is pressed. 

{% include note.html type="warning" title="Microcontrollers, Sketches and Power" text="Every microcontroller has memory which stores the programs you put on it. Even if you remove the power the microcontroller still stores that program. When you plug it into power, it retrieves this program from memory and starts to run it again.<br/><br/>Only when you put a new program on the controller will the last one stop running." %}



Within the setup function, the microcontroller expects us to tell us how we want to use it. One of the most common things to do, is declare how the pins will be used. Digital Pins (and some other pins) can be used for input and output. So when we want to use a PIN we first need to say which of the two it will be used for.  

The first command in our program does exactly this. 

````
void setup() {
  // We want to tell the Photon that we'll use
  // D0 as an output pin.
  pinMode(ledPin, OUTPUT);
}
````

Remember that <code>ledPin</code> is a variable that maps to the digital pin zero (<code>D0</code>). 

pinMode is a function that let’s us say what the pins will do. It takes two parameters or variables that can be passed to it: the pin we are dealing with, and if it will be used for <code>INPUT</code> or <code>OUTPUT</code>. To find out more look at: [http://arduino.cc/en/Reference/pinMode](http://arduino.cc/en/Reference/pinMode)


{% include note.html type="warning" title="Functions + Curly Braces" text="Setup is a function. Every function will begin with an opening curly brace and finish with a closing curly brace. Everything in between is part of the function. " %}

{% include note.html type="warning" title="Finishing your lines" text="Notice how every line that does something in the program ends with a semicolon, ‘;’. This is really important. This tells the compiler that the line is terminated or that we are finished telling the the microcontroller about one of the things it should do.<br>__If you forget to add a semicolon you will get errors when you compile.__" %}


**A note on <code>digitalWrite</code>**

We’re going to use a command called digitalWrite to control the pin at <code>D0</code>. It’s called a digital pin because its basically like binary, its either a 0 or a 1, on or off or in microcontroller speak "<code>HIGH</code>" or “<code>LOW</code>”. 

A pin is basically like a faucet. Its connected to power from the USB that we plug in. This is like a pump. When can turn the faucet (pin) on, water (electricity) will flow out down the pipes (or wires). When you turn the faucet off, the flow stops. Simple.

<code>digitalWrite</code> takes two parameters or passed variables which tell it the pin we want to control and what the power should be set to (<code>HIGH</code> or <code>LOW</code>). See: [http://arduino.cc/en/Reference/digitalWrite](http://arduino.cc/en/Reference/digitalWrite)

### Step 4: Making it Blink

This is where the good stuff happens. 

We’ve already setup our sketch. Now we need to fill in the <code>loop()</code> function. Loop gets called over and over and over and over. Once <code>setup()</code> finishes the microcontroller next executes everything inside the curly braces of the loop function. When it gets to the end (the closing curly brace), it will pause for a moment (about 5 milliseconds, a very long time for a computer) and then start all over again. 

To make the LED blink we’re going to do the following

1. We’re going to turn the power on (set it to <code>HIGH</code>)

2. we’re going to wait a second so that you can see the led on

3. then we’re going to turn it off again

4. we’re going to wait a second so you can see it off

5. then we’re going to let the loop loop over and over 

So does this look in computer speak:

````
void loop() {
  // First... On
  digitalWrite(ledPin, HIGH);   // Turn ON the LED pins
  delay(1000);               // Wait for 1000mS = 1 second

  // Now... Off
  digitalWrite(ledPin, LOW);   // Turn OFF the LED pins
  delay(1000);               // Wait for 1000mS = 1 second
  // rinse + repeat

}
````

Let’s break this down:

* <code>digitalWrite(ledPin, HIGH)</code> turns our LED on.

* We use the <code>delay</code> function which takes an integer/number expressed as milliseconds (1000 seconds) to make the controller wait for a bit before moving onto the next line.

* <code>digitalWrite(ledPin, LOW)</code> turns our LED off.

* Then we delay again.

Looks like we’re ready to put this program on your microcontroller. 


{% include note.html type="warning" title="// Comments - Making programs human readable" text="Any text beginning with // is ignored. These lines are comments, which are notes that you leave in the program for yourself, so that you can remember what you did when you wrote it, or for somebody else, so that they can understand your code." %}



## Step 5: Compiling and sending to the Particle device

Make sure the Status Bar has a device connected and the photon’s indicator is breathing blue. If not make sure your Photon is connected by USB and is getting a WiFi signal.

Press the Lightning bolt on the top left of the window. 

**[If the Lightning bolt is disabled / greyed out, you might not have saved your sketch - see Step 2 for details]**

You’ll see a message ‘Compiling in the Cloud’ and a few sections later your Photon should start flashing magenta.

Wait a few moments, it should return to breathing blue, and the LED should begin to flash!

## Step 6: Congratulations

You’ve just build your first circuit and written your first program to make it interactive. Below are some ways you can take it further. 

## Build your skills - Independent Exercises

Now let’s go beyond the basics and begin to explore how to develop circuits and control them. Below are three exercises that you can do to begin building skills.


{% include note.html type="tip" title="Exercise 1" text="Modify the program to Blink on and off every 3 seconds.<br/><br/>Hint: You only need to make two changes. Read the comments to see where." %}

---

{% include note.html type="tip" title="Exercise 2" text="Change the program to blink on and off 5 times then stop for 3 seconds. Each blink should be 0.5s (a half second)<br/><br/>Hint: An easy way to do this is to copy and paste. A better way to do this is with a for loop!" %}

---

{% include note.html type="tip" title="Exercise 3" text="Go back to the original program. Now add a second LED to the circuit.<br/><br/>Program the LED’s to alternate blinks i.e. when LED 1 turns on, LED 2 turns off, then when LED 2 turns on, LED 1 turns off." %}



