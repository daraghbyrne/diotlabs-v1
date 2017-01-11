---
layout: page
title: "Using the In Built RGB on your Board"
---


Particle offers a [library](../libraries) to control the RGB LED that’s built into the Particle board.

There are two main functions from a Library called LED that we’ll use. These are

* <code>RGB.control(true|false);</code> - lets us take control and return control of the RGB to the board / normal functions 

* <code>RGB.color( r,g,b)</code> - allows us to set the color of the RGB led on the board.

__Note__, we don’t need to create a circuit for us. It’s already hard wired from the previous example.

## Step 1: Setting up the Sketch 

We’re going to quickly modify the RGB example to allow you to control the LED online. 

The full code can be found at: [{{site.github_source_code}}]({{site.github_source_code}})

####  Add your variables

We don’t need to map any pins for this, so we just create variables to store your red, green and blue values like so.

````
int redValue = 255; // Full brightness for an Cathode RGB LED is 0, and off 255
int greenValue = 255; // Full brightness for an Cathode RGB LED is 0, and off 255
int blueValue = 255; // Full brightness for an Cathode RGB LED is 0, and off 255
````

#### Setup <code>setup()</code>

The only thing we really need to do here is register the function. Everything else can go. 

````
void setup()
{
  //Register our Particle function here
  Particle.function("led", ledControl);
}
````

####  Still no <code>loop()</code>

We still don’t need a loop because all of our functionality will be in a cloud function.


````
void loop()
{
   // Nothing to do here
}
````


#### The Main Method

While there’s nothing in loop we do need to have some functionality to control a light. 

Our function is called <code>ledControl</code>. It returns an <code>integer</code> and it takes one parameter called <code>command</code>

````
// This function gets called whenever there is a matching API request
// the command string format is <red>,<green>,<blue>
// for example: 255,0,128 or 128,0,0

int ledControl(String command)
{

    String colors[3];
    // ..[see previous for full code]..
    blueValue = colors[2].toInt();


    // We need to say we'll be controlling the RGB led
    RGB.control(true);

    // set it to white
    RGB.color( redValue,greenValue,blueValue);

    // wait 3 seconds
    delay( 3000 );

    // return control of the RGB led to Particle
    RGB.control(false);


   return 1;
}
````


This is almost the same as last time but with a few changes at the end of the code.

Once we’ve parsed out the red, green and blue values, we need to do the following:

First we tell the board we want to use the RGB led that's built in. We do this with:

````
RGB.control(true);
````

Once we  have control, we need to set the colors that we want to appear

````
RGB.color( redValue,greenValue,blueValue);
````

And then after waiting a couple of seconds, we do the nice thing and release the LED so that the microcontroller can tell us what’s happening (though we dont’ have to do this. 

````
RGB.control(false);
````

… and then we wait for the next command.

## Step 3: Controlling your Light.

There’s two ways to control your light. The easy way is through Particle Dev, and then you can make a RESTful API call. We’ll do both.

#### 3.1 Using Particle Dev.

Select the Particle menubar item, and choose the ‘Show Cloud Functions’ option (2nd from the bottom) and the following screen will appear. 


{% include figure.html src="../images/builtinrgb_0.png" caption="Particle Build Panel" class="" %}

Now to check your Particle function! 

You should see a text box beside your function named led. Just type HIGH or LOW into the box. The box marked ‘Result’ beside the == sign will show a spinning indicator for a second and then your light should respond as expected.

#### 3.2  Using the REST API

* Open up [http://build.particle.io/](http://build.particle.io/)

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

####  3.3 Use the CLI

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

####  3.4 Use the Web Page

* Open up RGBControl.html 

* Enter your devices information and your access token

* Drag the sliders

