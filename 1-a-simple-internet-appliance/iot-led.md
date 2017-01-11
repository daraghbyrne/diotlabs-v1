---
layout: page
title: "Making a Connected LED"
---

Now let’s transform our basic LED circuit into an online connected internet appliance - a light you can switch on and off from anywhere

## Step 1: Create your Circuit

The circuit, wiring and components are identical to the [last time](../first-sketch). 

{% include figure.html src="../images/iot-led-0.png" caption="Circuit Diagram for our LE" class="" %}

## Step 2: Setting up the Sketch 

Let’s get the basics of our sketch underway.

**Add your variables**

We’re going to use D0 again, so set up a variable that maps to that pin at the top of your sketch


````// name the pins
int ledPin = D0;
````

**Setup <code>setup()</code>**

Now, let’s specific the basics of our sketch. We need to configure pin D0 as output, but we also want to set up a starting state to make sure that the light is initially turned off.

````
void setup()
{
   // Configure the pins to be outputs
   pinMode(ledPin, OUTPUT);

   // Initialize both the LEDs to be OFF
   digitalWrite(ledPin, LOW);
}
````

**What happened to <code>loop()</code>**

In this case, all of the heavy lifting is going to be handled by an internet connected function. We don’t need the Particle Photon to do anything during the loop so we leave this totally blank.

````
void loop()
{
   // Nothing to do here
}
````

**The Main Method**

While there’s nothing in <code>loop</code> we do need to have some functionality to control a light. 

Our function is called <code>ledControl</code>. It returns an integer and it takes one parameter called command

````
int ledControl(String command)
{
   int state = LOW;

   // find out the state of the led
   if(command == "HIGH"){
	   state = HIGH;
   }else if(command == "LOW"){ 
	   state = LOW;
   }else{
	   return -1;
   }

   // write to the appropriate pin
   digitalWrite(ledPin, state);
   return 1;
}
````

Let’s walk through what is happening here.  The function starts with a string (some text) being passed to it from the internet or elsewhere in the code. 

We’re going to use this string to make some decisions as to what we should do. Based on what is sent in the string we will either turn the LED on or turn it off.

While we’re making decisions we need a place to store that decision. That’s why an integer variable called ‘state’ is declared. Its initialized (or set) to <code>LOW</code>.

Now we need to make some decisions. For this we use an <code>if...else if...else</code> statement. This uses ‘conditional logic’ to make a series of logical choices based on the information provided. 

You see that the if part has some information inside the parentheses i.e. <code>(...)</code>. This is called the condition. This basically checks if the condition comes out to be true or false. If the condition is true, everything inside its curly braces is executed, otherwise it skips to the next point. 

In other words it makes evaluations based on logic. In this case we are testing equality: if the string passed is the same as the string on the other side of the == signs.The  ‘==’ denotes an equality test.

This <code>if...else if...else</code> statement says:

1. If a string with the value of ‘<code>HIGH</code>’ is passed, set the state variable to ON/HIGH

2. If a string with the value of ‘<code>LOW</code>’ is passed, set  the state variable to OFF/LOW

3. If some other string is passed, we want to ignore it. We use the return statement to exit the function. We also know the function must provide an integer response so here we send back -1 to indicate something went wrong.

Finally, if a value of ‘<code>HIGH</code>’ or ‘<code>LOW</code>’ was received we’ll want to act on it. We use the digitalWrite function to turn the pin on or off depending what was received. After that we return an integer value of 1 to indicate everything was successful.

{% include note.html type="hint" title="Conditions" text="There are several different types of condition which can be checked.  We covered equality (==), but there is also inequality (!=) which checks if two item don’t match. For numbers we can also see if there are more (>) or less (<) than another value, as well as more than or equal to (>=) and less than or equal to (<=)<br/><br/>Read more at: [http://arduino.cc/en/Tutorial/IfStatement](http://arduino.cc/en/Tutorial/IfStatement) and [http://arduino.cc/en/Reference/if](http://arduino.cc/en/Reference/if)" %}


{% include note.html type="hint" title="Conditions" text="If your conditions only execute one line of code you can simplify your statements and remove the curly brackets surrounding them e.g. <code> if(command == \"HIGH\")    state = HIGH;</code>. But it's generally good practice to include them!" %}



**Finally, add the cloud function**

The last thing we need to do is connect the Particle cloud to the function we have just written. We do this by adding a single line to the setup() function.

````
void setup()
{
   //Register our Particle function here
   Particle.function("led", ledControl);

...
````

Adding this one line makes the function ledControl available as "led" on the Particle cloud. 

## Step 3: Compiling and sending to the Particle Photon.

Make sure the Status Bar has a Particle Photon connected and the Particle Photon’s indicator is breathing blue. If not make sure your Photon is connected by USB and is getting a WiFi signal.

Press the Lightning bolt on the top left of the window. 

You’ll see a message ‘Compiling in the Cloud’ and a few sections later your Photon should start flashing magenta.

Wait a few moments, it should return to breathing blue, and the LED should be off.

## Step 4: Controlling your Light.

There’s two ways to control your light. The easy way is through Particle Dev, and then you can make a RESTful API call. We’ll do both.

#### Using Particle Dev.

Select the Particle menubar item, and choose the ‘Show Cloud Functions’ option (2nd from the bottom) and the following screen will appear. 

{% include figure.html src="../images/iot-led-1.png" caption="Particle Dev's Cloud Function Panel" class="" %}

Now to check your Particle function! 

You should see a text box beside your function named led. Just type HIGH or LOW into the box. The box marked ‘Result’ beside the == sign will show a spinning indicator for a second and then your light should respond as expected.

####  Using the REST API 

* Open up [http://particle.io/build](http://particle.io/build)

* Select the Target Icon to view your Particle devices. Select the device which is currently connected and the device ID information will appear.

* Copy down the device ID - you’ll need that in a second.

* You also need an Access Token. To get that click on the ‘Settings’ icon. You’ll see an access token string. Copy this down too.

* Modify the below and paste it into a Terminal Window

````
curl https://api.particle.io/v1/devices/[deviceID]/led -d access_token=[access_token] -d params=HIGH
````

You will get a response like

````
{
  "id": "3432094809234802938498230948239",
  "name": "ParticleBoardName",
  "last_app": null,
  "connected": true,
  "return_value": 1

````

__Congratulations! You just put your LED on the internet!__

---

## Build your skills - Independent Exercises

{% include note.html type="tip" title="Exercise 1" text="Modify the cloud function to blink the LED 3 times after it is called" %}

---

{% include note.html type="tip" title="Exercise 2" text="Modify the cloud function as follows:<br/><br/>Instead of passing a <code>HIGH</code> Or <code>LOW</code> string pass the number of times you would like it to blink<br/> Set the function to blink that number of times<br/> Finally once it has completed all of the blinking it should turn the LED off" %}

---

{% include note.html type="tip" title="Exercise 3" text="Go back to the original program. Now add a second LED to the circuit.<br/><br/>Change the program and cloud function to allow you to control both LEDs remotely" %}




