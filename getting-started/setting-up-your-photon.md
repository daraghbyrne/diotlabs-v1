---
layout: page
title: "Setting up your Particle Photon"
---

This is a super quick overview of the steps you'll need to take to get your Photon board up and running. You'll need:

- A Particle Photon 
- The USB cable
- A laptop / desktop computer (Windows or Mac)
- An internet connection (and potentially a connection on your mobile phone too)

This is a quickstart guide for using [Particle Dev](https://www.particle.io/dev), connecting it to the CMU network for the first time, and claiming your device. 

There are a few other ways to get your device online. If you're using your own personal network, these are quicker and easier:

- Using [this guide](https://docs.particle.io/guide/getting-started/start/photon/#step-2-connect-with-your-smartphone), You can use the [Particle Tinker app](https://docs.particle.io/guide/getting-started/tinker/photon/) on your Smartphone to directly connect with the Photon and give it the WiFi network information. 


- You can also use the [command line interface (CLI)](https://docs.particle.io/guide/tools-and-features/cli/) from Windows, OSX and Linux to manage and configure your devices. Once [installed](https://docs.particle.io/guide/tools-and-features/cli/#installing), just call <code>particle setup</code> and follow the instructions. 


- There's also detailed guides provided by Particle and if you run into trouble, it will be worth lookin at [their connecting your photon guide](https://docs.particle.io/guide/getting-started/connect/photon/)

# Starting the Setup

Let's follow these steps for a *hopefully* headache free installation which will let you use the CMU network with your particle. 

{% include note.html type="note" title="Some notes" text="This guide (and all subsequent tutorials and guides) assumes you're using the the downloadable IDE (interactive development environment. [Particle Dev](https://www.particle.io/dev) is awesome - it's got tonnes of really nice features for developing IoT solutions and working with the Particle cloud. I highly recommend it. <br/><br/>But Particle also have an online web client that allows you to write code, work with libraries and flash programs to your device: [Particle Build](https://build.particle.io/). If you're planning to use the web client, that's great, but please see the documentation on the Particle.io - [https://docs.particle.io/guide/getting-started/start/photon/](https://docs.particle.io/guide/getting-started/start/photon/)" %}



{% include figure.html src="../images/setup/image06.jpg" caption="Plug it in!" class="small right" %}


# Step 1. Plug in Your Particle Photon

- Connect your core to your computer using the USB cord.

- The Core’s light will flash Blue. This means it doesn’t know how to connect to the Wireless network… yet.

**Hold on it’s not blinking blue...**

- Hold down the SETUP button (button to the left of the main LED) until it starts blinking blue. 

# Step 2: Download  Particle Dev

- Visit [https://www.particle.io/dev](https://www.particle.io/dev) and download the software. It’s available for Windows and Mac.

- Once downloaded, unzip the download and move "Particle Dev" to your Applications folder.

- Launch the application.


{% include note.html type="tip" title="Tip" text="Detailed information on using Particle Dev is at: [http://docs.particle.io/dev/](http://docs.particle.io/dev/)." %}

{% include note.html type="warning" title="Windows Users" text="You'll also need to install the Windows driver <br />Download: [Windows driver for Particle photon](https://s3.amazonaws.com/spark-website/Particle.zip)<br/>When you have it downloaded, [follow these instructions](https://docs.particle.io/guide/getting-started/connect/photon/#installing-the-particle-drive)."%}

# Step 3: Open Particle Dev

You should see something like this. 

{% include figure.html src="../images/PaticleDev-ShowSerial.jpg" caption="Particle Dev Interface" class="" %}

This is where the fun begins because the CMU network doesn’t play nice with devices. In order to get a device on the network we need to know its MAC address and to know its MAC address we need to have it on the network. Yowsers!

First, we need to find out a little information about our device. We need the 
1. **Device ID** - This is what the Particle Cloud knows the device as. It's a big long string of letters and numbers that uniqiely identifies it. We don't need to know this but we do need it to get our Particle device connected to the cloud.
2. **Mac Address** - This is what a wireless network knows the device as. It's a unique identifier for the hardware we're putting on the network. We need to know this to put the device on the CMU network.

To get this information, open the **Serial Monitor** as shown in the image above.

- Click on the Particle menu (top right) and select the 'Show Serial Monitor' option. A new panel will open. 

- Then select your USB port. It'll look something like <code>/dev/cu.usbmodem1411</code> and click **Connect**.

- Type <code>i</code> in the text entry field at the bottom that says *"Enter string to send..."*

- Some text should appear. Bingo. You just got the __*identity*__  of the device

- Type <code>m</code> in the text entry field at the bottom that says *"Enter string to send..."*

- Some text should appear. Awesome. You just got the __*mac*__ address of the device

{% include figure.html src="../images/SerialCommspanel.jpg" caption="Mac address and Identity of your particle device" class="" %}

{% include note.html type="note" title="Keep it safe" text="You'll need this information again and it's important. Copy and paste it to a text file for safe keeping."%}

{% include note.html type="warning" title="Not working or not displaying information?" text="If your device isn't returning any information, there's a couple of things to try<br/><br/>__First, is it in listening mode?__ To check, just make sure the LED on your device is blinking deep blue. If its not, just hold down the <code>SETUP</code> button for 3-5 seconds and try the steps again. <br/><br/> __Second, you might need to update your firmware__ Firmware is the stuff that makes the board work - it monitors, controls and interfaces with the hardware, and it interprets the code you send it to make it work. Sometimes it needs to be updated to add new functionality or to patch problems. The easiest way to do this is to [install the Particle CLI](https://docs.particle.io/guide/tools-and-features/cli/). Once installed, put the device in the [DFU mode](https://docs.particle.io/guide/getting-started/modes/photon/#dfu-mode-device-firmware-upgrade-). <br><br/> To do this, hold down the <code>SETUP</code> and <code>RESET</code> buttons together, then release the <code>RESET</code> button. Wait a couple of seconds and the LED on the board will begin to flash yellow. When it does release the <code>SETUP</code>. It should stay pulsing yellow. If it doesn't or it's another color, press reset and try again! <br/><br> Then go to the command line and type <code>particle update</code><br/><br/> If all goes well your device will have the current firmware in 30 seconds, then you can try the above again!" %}



# Step 3: Register your device's Mac Address with the CMU Network

* Go to [https://netreg.net.cmu.edu/](https://netreg.net.cmu.edu/)  click enter and sign in with your CMU credentials.

* Click the "Register New Machine" link.

* Under "Network", select “Wireless Network” and click continue.

* Choose a host name for your machine’s DNS. Copy that url. for example: DARAGHSSPARKCORE.WV.CC.CMU.EDU

* Enter the hardware address you copied earlier in the Hardware Address field and click continue.

{% include note.html type="warning" title="Hold tight" text="It can take about an hour for your adapter to be registered with the network!" %}

{% include note.html type="tip" title="Hold tight" text="You don't need to do this part everytime you connect your Particle device; just the _first time_ you want to use it on the CMU network." %}

The next step will be to register (or claim) our device on the Particle Cloud. Unfortunately, you've got to wait until the NetReg piece is finished, before you can do this.  

While we're waiting, let's create an account for Particle's cloud. 


# Step 4: Sign Up for Particle Cloud

Open your web browser, and create an account on Particle 
- Go to: [https://build.particle.io/signup](https://build.particle.io/signup)
- Follow the on screen instructions

This will also give you access to the online IDE ([Particle Build](http://particle.io/build)) which you can use to develop applications within your web browser.

{% include figure.html src="../images/setup/image05.png" caption="Log on" class="small right" %}

# Step 5: Add your Login Details to Particle Dev

- Launch Particle Dev (which you downloaded) and you will see a ‘Particle’ menu on the far right. 

- Click on this and you will see a dropdown asking you to ‘Log in to Particle Cloud’ 

- Add your newly created account information and click ‘Log In’

- Click on the menu again and you should see a bunch of options

You do?  __Great, we’re getting places...__

# Step 6: Connecting to WiFi

You’ve twiddled your thumbs and your network registration is applied and ready to roll.  Now, let’s set up the CMU WiFi Details on your Particle Photon. 

There's a couple of ways to get your device onto WiFi: 

#### a. RECOMMENDED: Using the Serial Monitor

- Open Particle Dev, and select the 'Show Serial Monitor' option.

- Connect to the serial monitor as before (see Step 3)

- Type the letter 'w' immediately followed by the SSID of the wireless network i.e. CMU (all upper case)

  ````
  wCMU
  ````
  
- You'll be asked the settings for the network's "Security 0=unsecured, 1 = WEP, 2=WPA, 3=WPA2". Type 0 (unsecured)

- The WiFi Settings will be applied. 

- If the device remains in the blinking blue (listening) mode, disconnect the USB power lead and plug it back in again. Works a charm!

{% include figure.html src="../images/ParticleDevMonitorWiFi.jpg" caption="Serial Monitor Setup process completed" class="" %}

#### b. Using Particle Dev (Caution!)

{% include note.html type="tip" title="Hold tight" text="This doesn't seem to work in the current version of Particle Dev, but will probably work again in a future release." %}

- In Particle Dev: Select the ‘Particle’ Menu and the the option to ‘Setup Devices WiFi’ (__note: __)

- It will scan for nearby WiFi signals, and select the hotspot or network you want to use. Select ‘CMU’ Wireless (not CMU-SECURE) 

- When selecting the SSID: For some reason, when you select the CMU SSID, it appears blank. Instead of pointing and clicking, you'll just type in the SSID manually. Make sure it's ALL CAPS too!

#### c. Using the Particle Command Line

If you've set up the [Particle CLI](https://docs.particle.io/guide/tools-and-features/cli/), simply type <code>particle setup wifi</code> and follow the prompts.

{% include figure.html src="../images/CLIWifiSetup.jpg" caption="Process for adding WiFi credentials to your Particle device through the CLI " class="" %}

#### d. Using the Particle Tinker App 

Open your smartphone, fire up the App, 

- To add a new device, click the '+' top right, select the 'Photon' as device, and follow the instructions. 
- Set the Wireless network as 
  - **SSID: CMU**
  - Authentication: None
  - Password: none
- If you do this, you can also skip the remaining sections, as it will help you claim your device too!

--- 

Now… Cross your fingers. In a few seconds, your Particle Photon should flash green then slowly pulse cyan. This means it’s connected to your WiFi network. Super!

{% include note.html type="warning" title="Having Trouble?" text="To set WiFi credientials your Particle device needs to be in listening mode. To check, just make sure the LED on your device is blinking deep blue. <br/><br/> If its not, just hold down the <code>SETUP</code> button for 3-5 seconds and try the steps again." %}

# Step 7: Claiming your core 

Your Particle’s online and we’re ready to claim your core. Essentially we're telling the Particle framework that this device belongs to your account and you're the only person who should be able to access it's data and send code to it. To do this we need:

1. to know what the device is called in computer speak, or its hexadecimal ID (see step 2)
2. to have the device connected to WiFi (see step 6)

Thankfully you've already got both of these... There's two ways you can 'claim' your core' using the Device ID - through Particle Dev on your desktop, or through the Build tool online. 

### Using Particle Dev.

Select the ‘Particle’ menu and choose ‘Claim Device’. Paste in the device ID, hit enter, and bobs your uncle, you now have a Photon linked to your account. 

When you open the Particle Menu in Dev now, you should see something like this. 

{% include figure.html src="../images/Claimed.jpg" caption="" class="Note that a list of devices is displayed in the dropdown menu" %}

<br/>

Now is a good time to name your device something memorable. Select "Rename xxxxxxxxxxx’ and add something in. If you have a problem naming it, you can always visit: [https://www.particle.io/build#cores](https://www.particle.io/build#cores) choose the cores option (bottom left) and add it via the online dashboard.

### Using the Online Build tool

- Visit: [https://build.particle.io/build#devices](https://build.particle.io/build#devices) choose the devices option (bottom left, looks like a cross-hairs) 

- Click the 'Add a new Device' button, paste in the device ID, and click to 'claim device'.

- Once added you can click on the name of any claimed device to rename it or view the device ID.


### Tah! Dah!

You're all set to start using your Particle Photon!


{% include note.html type="warning" title="Changing Places" text="If you leave campus and are working at home, or generally move places, remember that you're also going to be changing WiFi networks! If you change networks you need to tell your device about it. If you've moved location and the device is stuck flashing green or rapidly blinking blue, you probably need to set new WiFi credentials <br/><br/> Particle devices remember the last WiFi network they were connected to, but if you change networks __you have to tell it each time it should connect to a new or different network__. <br/><br/> To do this, just put the device in listening mode (blinking deep blue) by holding down the <code>SETUP</code> button for 3-5 seconds and follow the instructions in Step 6." %}
