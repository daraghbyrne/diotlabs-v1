---
layout: page
title: "Setting up your Particle Photon"
---

This is a super quick overview of the steps you'll need to take to get your Photon board up and running. You'll need:

- A Particle Photon 
- The USB cable
- A laptop / desktop computer (Windows or Mac)
- An internet connection (and potentially a connection on your mobile phone too)

There are much more comprehensive steps and guidance provided by Particle and if you run into trouble, it will be worth lookin at [their connecting your photon guide](https://docs.particle.io/guide/getting-started/connect/photon/)

{% include note.html type="note" title="Some notes" text="This guide (and all subsequent tutorials and guides) assumes you're using the the downloadable IDE (interactive development environment. [Particle Dev](https://www.particle.io/dev) is awesome - it's got tonnes of really nice features for developing IoT solutions and working with the Particle cloud. I highly recommend it. <br/><br/>But Particle also have an online web client that allows you to write code, work with libraries and flash programs to your device: [Particle Build](https://build.particle.io/). If you're planning to use the web client, that's great, but please see the documentation on the Particle.io - [https://docs.particle.io/guide/getting-started/start/photon/](https://docs.particle.io/guide/getting-started/start/photon/)" %}


{% include figure.html src="../images/setup/image06.jpg" caption="Plug it in!" class="small right" %}

# Step 1. Plug in Your Particle Photon

- Connect your core to your computer using the USB cord.

- The Core’s light will flash Blue. This means it doesn’t know how to connect to the Wireless network… yet.

*Hold on it’s not blinking blue...

- Hold down the MODE button (button to the left of the main LED) until it starts blinking blue. 

# Step 2: Download  Particle Dev

- Visit [https://www.particle.io/dev](https://www.particle.io/dev) and download the software. It’s available for Windows and Mac.

- Once downloaded, unzip the download and move "Particle Dev" to your Applications folder.

- Launch the application.


{% include note.html type="tip" title="Tip" text="Detailed information on using Particle Dev is at: [http://docs.particle.io/dev/](http://docs.particle.io/dev/)." %}

{% include note.html type="important" title="Windows Users" text="You'll also need to install the Windows driver: Windows driver for Particle Photon <br />[Windows driver for Particle photon](https://s3.amazonaws.com/spark-website/Particle.zip)<br/>When you have it downloaded: <br /> Go to Device Manager → Find Particle Photon Wifi → update devices → manually select the Particle folder you just downloaded." %}


# Step 3: Sign Up for Particle Cloud

Open your web browser, maybe while the application is downloading and visit [https://build.particle.io/signup](https://build.particle.io/signup)

Create an account on Particle and follow the instructions.

This will also give you access to the online IDE which you can use to develop applications without the desktop IDE.

{% include figure.html src="../images/setup/image05.png" caption="Log on" class="small right" %}

# Step 4: Add your Login Details

Launch Particle Dev (which you downloaded) and you will see a ‘Particle’ menu on the far right. 

Click on this and you will see a dropdown asking you to ‘Log in to Particle Cloud’ 

Add your newly created account information and click ‘Log In’

Click on the menu again and you should see a bunch of options

You do?  Great we’re getting places

Step 5: Identifying your core

We need to tell the Particle framework that this Core belongs to your account. To do this we need to know what the Core is called in computer speak, or its hexadecimal ID. Go back to the IDE, select the ‘Particle’ menu and choose ‘Identify Device’

You should see a box with a big long string appear, something like: 

<pre>54ff6c066667515122431567</pre>

Copy and Paste this String and keep it somewhere safe. We’ll use it again in a minute.

# Step 6: Claiming your core and Connecting to the CMU Network

This is where the fun begins because the CMU network doesn’t play nice with devices. In order to get a device on the network we need to know its MAC address and to know its MAC address we need to have it on the network. Yowsers!

We need a workaround… and that is to use a hotspot! 

**Best Option:** If you have an iPhone or iPad handy, open ‘Settings’ > ‘Personal Hotspot’, turn your personal hotspot on and add a WiFi password. Check your hotspot appears in the WiFi network dropdown on your Mac’s menu bar 

[PST… Perhaps a nice iPhone user will let you use theirs?]

**Option 2:** If you’re connected to an Ethernet port (wired internet) use your Mac to Share your internet connection - see: [http://www.imore.com/how-turn-your-macs-internet-connection-wifi-hotspot-internet-sharing](http://www.imore.com/how-turn-your-macs-internet-connection-wifi-hotspot-internet-sharing)

**Option 3:** Perform this step on your home network or any network other than the CMU network!

### So…

{% include figure.html src="../images/setup/image07.png" caption="" class="medium right" %}


We’ve got a network. Let’s say its ‘Daragh’s Phone’ with a password of ‘brute1234’

First, let’s set up the WiFi Details for the Particle Photon. Select the ‘Particle’ Menu and the option to ‘Setup Devices WiFi’

It will scan for nearby WiFi signals, and select the hotspot or network you want to use. Then enter the password (for a Hotspot or normal WiFi WPA2 should be selected) or select ‘Unsecured’ if there is no password. 

{% include figure.html src="../images/setup/image04.png" caption="" class="medium right" %}


Now… Cross your fingers. In a few seconds, your Particle Photon should flash green then slowly pulse cyan. This means it’s connected to your WiFi network. Super!

But we’re not done yet…

### Claiming your Core

Your Particle’s online and we’re ready to associate your account to this Core. 

Select the ‘Particle’ menu and choose ‘Claim Device’. Paste in the number from the previous and bobs your uncle, you now have a Photon linked to your account. 

When you open the Particle Menu now, you should see something like this.

{% include figure.html src="../images/setup/image00.png" caption="" class="Note that a list of devices is displayed in the dropdown menu" %}

<br/>

Now is a good time to name your core something memorable. Select "Rename xxxxxxxxxxx’ and add something in. If you have a problem naming it, you can always visit: [https://www.particle.io/build#cores](https://www.particle.io/build#cores) choose the cores option (bottom left) and add it via the online dashboard.

### *phew*, nearly there I promise…

Getting your Mac Address

1. Go to the Particle Dev Application. 

2. Select ‘File’ and ‘New Window’

3. Cut and Paste the code below into it

4. Save the file as ‘MacAddress.ino’ in a folder called ‘MacAddress’ Note: the .ino is really important!

5. Click the Lightning icon on the top left

6. The core will flash magenta for a few seconds, then return to blue

7. From the ‘Particle’ Menu select ‘Show Cloud Variables’ (2nd option from the bottom) 

8. You’ll see a screen like the one below (hit refresh if it says 0:0:0:0:0)

9. Copy the Value and save it for later

```
byte mac[6];
char macstr[18];

void setup() {

  WiFi.on();
  WiFi.connect();

  Spark.variable("mac", macstr, STRING);

  WiFi.macAddress(mac);

  snprintf(macstr, 18, "%02x:%02x:%02x:%02x:%02x:%02x", mac[5], mac[4], mac[3], mac[2],mac[1], mac[0]);

}

void loop() {
  snprintf(macstr, 18, "%02x:%02x:%02x:%02x:%02x:%02x", mac[5], mac[4], mac[3], mac[2],mac[1], mac[0]);
}
```

{% include figure.html src="../images/setup/image01.png" caption="Code entered into the Particle Dev IDE" class="" %}

<br/>


{% include note.html type="note" title="BTW" text="Nice work! Believe it or not, you just wrote your first application for Particle Photon!" %}


### Register your device's Mac Address with the CMU Network

* Go to [https://netreg.net.cmu.edu/](https://netreg.net.cmu.edu/)  click enter and sign in with your CMU credentials.

* Click the "Register New Machine" link.

* Under "Network", select “Wireless Network” and click continue.

* Choose a host name for your machine’s DNS. Copy that url. for example: DARAGHSSPARKCORE.WV.CC.CMU.EDU

* Enter the hardware address you copied earlier in the Hardware Address field and click continue.

{% include note.html type="warning" title="Hold tight" text="It can take about an hour for your adapter to be registered with the network!" %}

### Add the 'CMU' network as a WiFi Access Point

You’ve twiddled your thumbs and your adapter is finally registered.  Now, let’s set up the CMU WiFi Details on your Particle Photon. 

Select the ‘Particle’ Menu and the the option to ‘Setup Devices WiFi’

It will scan for nearby WiFi signals, and select the hotspot or network you want to use. Select ‘CMU’ Wireless (not CMU-SECURE) 

{% include note.html type="note" title="Selecting the SSID" text="For some reason, when you select the CMU SSID, it appears blank. Instead of pointing and clicking, you'll just type in the SSID manually. Make sure it's ALL CAPS too!" %}

**=> SSID: CMU**

Now… Cross your fingers. In a few seconds, your Particle Photon should flash green then slowly pulse cyan. This means it’s connected to your WiFi network. Super!

### Tah! Dah!

