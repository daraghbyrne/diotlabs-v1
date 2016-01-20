---
layout: page
title: "Making a Connected Color LED"
---

We’re going to make an RGB LED that you can control from a webpage

## Step 1: Create your Circuit

The circuit, wiring and components look like this. Connect the red terminal to <code>A0</code>, connect the green to <code>D0</code> and the blue to <code>D1</code>. All should be connected to 1KOhm resistor. Finally connect the common anode to the power (3v3). 

{% include figure.html src="../images/using_rgbs_0.png" caption="RGB LED Circuit Diagram" class="" %}

## Step 2: Setting up the Sketch 

Let’s get the basics of our sketch underway.

#### Add your variables

Map your red pin to <code>A0</code>, your green pin to <code>D0</code> and your blue pin to <code>D1</code>. All of these pins have PWM control.

Then create variables to store your red green and blue components. We’ll use this later.

````
int redPin = A0;    // RED pin of the LED to PWM pin **A0**
int greenPin = D0;  // GREEN pin of the LED to PWM pin **D0**
int bluePin = D1;   // BLUE pin of the LED to PWM pin **D1**
int redValue = 255; // Full brightness for an Cathode RGB LED is 0, and off 255
int greenValue = 255; // Full brightness for an Cathode RGB LED is 0, and off 255
int blueValue = 255; // Full brightness for an Cathode RGB LED is 0, and off 255</td>
````

#### Setup <code>setup()</code>

Now, let’s specific the basics of our sketch. 

First let’s set our pins as being used for output. We also need to register a function we’ll create later to allow us to set the R,G,B values through an API.

Finally, let's set up our RGB led so all of the pins are turned off.

````
void setup()
{
  // Set up our pins for output
  pinMode( redPin, OUTPUT);
  pinMode( greenPin, OUTPUT);
  pinMode( bluePin, OUTPUT);

  //Register our Particle function here
  Particle.function("led", ledControl);

  // turn them all off...
  analogWrite( redPin, redValue);
  analogWrite( greenPin, greenValue);
  analogWrite( bluePin, blueValue);

}
````


#### What happened to a <code>loop()</code>

In this case, all of the heavy lifting is going to be handled by an internet connected function. We don’t need the Particle device to do anything during the loop so we leave this totally blank.

````
void loop()
{
   // Nothing to do here
}
````


#### The Main Method

While there’s nothing in loop we do need to have some functionality to control a light. 

Our function is called <code>ledControl</code>. It returns an integer and it takes one parameter called <code>command</code>


````
int ledControl( String command )
{
    String colors[3];
    colors[0]="";
    colors[1]="";
    colors[2]="";

    int index = 0;
    for( int i = 0; i < command.length(); i++ )
    {
      if( index < 3 ){
        char c = command.charAt(i);
        colors[index] += c;

        if( c == ',') index++;
      }
    }

    // get the red component...
    redValue = colors[0].toInt();
    // now green
    greenValue = colors[1].toInt();
    // now blue
    blueValue = colors[2].toInt();

   // write the mixed color
   analogWrite( redPin, redValue);
   analogWrite( greenPin, greenValue);
   analogWrite( bluePin, blueValue);

   return 1;
}
````


This is a little more complicated than usual so let’s talk about what’s happening here.

We need to be able to split the params in order to get the red, green and blue integers that were passed, but the Arduino language doesn’t give us an easy way to do this, so we have to improvise!

We create an array to hold the strings and we’re going to go character by character through the string to check what kind of character we get back.

The for loop is set up to loop for however many times the string is long. For each character in the string, we check to see if it is a comma. The comma is our delimiter or what separates our parameters.

If we have any value other than a comma, we append it to one of the string arrays. Each time we encounter a comma we move to the next string array. For instance, we start with the first string in the array (storing the red variable), when we get to the first comma, we then move to the next string - which stores the green component. 

Once we have all of the parts of the string separated we then convert them to integers, put them in the correct variables and then use analogWrite to set the correct value to each of our pins. 

## Step 3: Controlling your Light.

There’s a few ways to control your light - choose any of them that makes sense for your setup! The easy way is through Particle Dev, or to make a RESTful API call. These are illustrated below!

#### 3.1 Using Particle Dev.

Select the Particle menubar item, and choose the ‘Show Cloud Functions’ option (2nd from the bottom) and the following screen will appear. 

{% include figure.html src="../images/using_rgbs_1.png" caption="" class="" %}

Now to check your Particle function! 

You should see a text box beside your function named led. Type r g and b values into the text box as a series of comma separated numbers (e.g. 255,255,255 or 128,0,55) and press enter. The box marked ‘Result’ beside the == sign will show a spinning indicator for a second and then your light should respond as expected.

#### 3.2 Using the REST API 

* Open up [http://build.particle.io](http://build.particle.io/)

* Select the Target Icon to view your devices. Select the device which is currently connected and the device ID information will appear.

* Copy down the device ID - you’ll need that in a second.

* You also need an Access Token. To get that click on the ‘Settings’ icon. You’ll see an access token string. Copy this down too.

* Modify the below and paste it into a Terminal Window

````
curl https://api.particle.io/v1/devices/[deviceID]/led -d access_token=[access_token] -d params=255,0,0
````

You will get a response like

````
{
  "id": "3432094809234802938498230948239",
  "name": "ParticleDeviceName",
  "last_app": null,
  "connected": true,
  "return_value": 1

````

#### 4.3 Use the CLI

If you have the command line interface installed you can call: 

This will let you see all of your devices and the currently available functions:
````
particle function list
````

If you want to call one of them you do the following

````
particle function call [device_id] [function_name] [param1] [param2]
e.g.
particle function call 360031000447343232363230 led 255,0,0

````

#### 3.4 Use the Web Page 

* Open up RGBControl.html 

* Enter your devices information and your access token

* Drag the sliders

