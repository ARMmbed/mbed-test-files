<a name="intro"/>
#BLE for Designers
</a>

BLE is an exciting technology that has a natural appeal for designers who are looking to create art or solve problems. If you're a designer, and you've never programmed anything, we're here to help you get your idea prototyped using BLE on mbed boards.

##BLE

BLE means Bluetooth Low Energy (or Bluetooth Smart). It is a short-range wireless communication method - it is how your car, clothes and home can talk to your phone and each other. The difference between BLE and the original Bluetooth standard is that BLE is specifically deigned to reduce power consumption; your BLE device may run for months or years on a coin-cell battery. 

You've probably met BLE in a fitness tracker or a smart TV, but the beauty of BLE is that it's simply a method of transferring data - any data. If you have a sensor, button or any other input method, your BLE device can receive input from them and transfer it to a phone, tablet or PC (and with the advent of BLIP - Bluetooth IP Support - directly to the internet). You can then use it with any application you can think of to store or analyse the information, and even send commands back to the device.

This two-way communication means that a single device can be used both to send information and to perform actions based on that information. You could [water your garden](http://www.hosepipeban.org.uk/hosepipe-ban-current-situation/) when the ground is dry, put a beacon with your details on your dog's collar, or flash a light when a car comes too close to your bicycle. You can do anything at all, so long as you have the right sensor and an appropriate BLE-enabled platform - like mbed.

##mbed

[mbed](http://developer.mbed.org) gives you three things: a platform, APIs for that platform, and a programming environment (compiler). 

The platforms are little boards with a processor, which have various capabilities like receiving input, generating output, storing small bits of information and so on. Some boards require an external BLE component, and [some](http://developer.mbed.org/platforms/mbed-HRM1017/) [have it](http://developer.mbed.org/platforms/RedBearLab-BLE-Nano/) [built-in](http://developer.mbed.org/platforms/Nordic-nRF51-Dongle/).

Because platforms are standard pieces of hardware, you need to be able to tell them what to do. mbed has created APIs - Application Program Interface - that let you order off the menu. For example, if you want to send something over Bluetooth, you don't need to know the exact commands and sequence of events; you just need to tell the API that you want to send something - we've made sure the API knows how to do it. This is called *abstraction*, and you'll run into that word quite often on our website. BLE has its own API, called BLE_API.

To tell the API what to do, you need a programming environment. BLE, like all other mbed capabilities, can be programmed using the [mbed Compiler](https://developer.mbed.org/compiler/). 

##The mbed Compiler

The compiler fulfils two main purposes: it gives you a programming environment (a place in which to write your code), and it can turn that code into something that the mbed platforms can work with (compile). The compiler can take the same code and compile it for different mbed platforms, meaning you can try out your project on different boards and pick the one that suits you best, without having to re-write your program. 

Programming for mbed is done in *C++*. Although you can get quite a lot done with BLE without learning C++, if you want to create something unique you might have to either learn C++ or find a programmer in our community (or among your friends) to collaborate with. 

We'll walk you through using the compiler as we get started on our [coding samples](#uribeaconsample).
___

<a name="what_to_do"/>
##What Does it all Do?
</a>

The combination of an mbed board, the extra components available to it and BLE capabilities means you can do pretty much anything you like (we'll discuss the limitations [later](#limitations)).

###Gathering Information

Any mbed device, with or without BLE capabilities, can gather information. It can do that with [sensors](http://developer.mbed.org/components/) for anything from [light](http://developer.mbed.org/components/cat/light/) to [touch](http://developer.mbed.org/components/cat/capacitive-touch/), or it can receive information from a computer. 

You could also get information directly from users by providing them some input mechanism, such as a mobile app or button. We'll talk about that later.

###Displaying Information

The first thing you can do with a BLE device is simply display information. You can do that with lights or a [display](http://developer.mbed.org/components/cat/display/), or you can send the information to a nearby Bluetooth-enabled device like a mobile phone.

The information can be the sensor input - for example, you could display the speed as provided by an [accelerometer](http://developer.mbed.org/components/cat/sensors-motion/) - or static information that you've programmed onto the device, like your own details. 

###Processing Information 

The two most common sources of information that you might want to process are the sensors and user input. In either case, there are two main paradigms for processing:

1. *Local processing* means the device itself processes the data and determines what to do. The simplest example is a thermostat, which knows to turn the heat on or off according to a room temperature input, and doesn't require further instructions from anywhere.

2. *Remote processing* means that you send the data to a different device to be handled there, and either wait for instructions from the remote device or simply go on gathering and sending data. For example, if you're trying to predict tomorrow's weather, the device will send data (temperature, barometric pressure etc) to a computer that can analyse it - the local device will simply not have the processing power to run a weather program. 

BLE is intended for low power devices, and so we'll never perform complex processing on the device - processing burns through batteries. We'll instead send the data elsewhere, and wait for a response. 

###Sending or Storing Information

If you want a small and power-efficient device, you probably don't want to store too much locally; send your information to a server instead (it doesn't have to be a web server; it can be your own computer, if it's set up correctly).

BLE is a short-range method, meaning you'll be able to send information over BLE only if your device and your destination are quite close. If they're further away, you'll need to use Ethernet (regular cable connection), WiFi or radio.

###Working With Apps or Websites

So if you can't store or process too much information with a BLE device, what is it good for?

The simplest way to use BLE is to advertise a small bit of information to any device in the area, without becoming interactive. For example, you could notify every user entering your shop that you'll be open till late this evening. There is no need for applications, webpages or any response from the users - it's similar to putting a notice on your door.

The fully interactive way to use BLE requires an app (mobile or web-based). The app not only does the processing and storing, it also provides users with an interface through which they can send commands back to the BLE device. A very common example is fitness apps on your phone that get your heart rate information from a BLE-based heart rate monitor. The heart rate monitor doesn't store or process information - it just gets your heart rate and sends it to the app, which shows it to the user and allows the user some control of the BLE device.

###URI Beacons and the Physical Web

Physical Web brings devices to the internet via websites (rather than device-specific applications), by using BLE as a business card that includes a link to the website; interactions with the device are performed via the website. Using websites rather than apps means that users don't have to install a new app for every device they want to interact with; the interaction is easier and more immediate.

The method used to provide the link is called [URI Beacon](http://developer.mbed.org/teams/Bluetooth-Low-Energy/code/BLE_URIBeacon/), and it will be the first example we'll [show you](#uribeaconsample) when we get to programming our BLE devices. A URI Beacon can be attached to anything that you might want to provide information about, or that you can provide any sort of interface for.

For example, the beacon can be attached to a vending machine that you might then control via the web interface the beacon sent you to. The web interface can let you make a large purchase (providing sodas for several people in one transaction) by letting you select several options and pay for them all at once.

###What's Meshing, and Does it Work?

Meshing means sending information from one BLE device to another, and at the moment there's no easy way of doing it with BLE. 

###What's FOTA, and Does it Work?

FOTA stands for Firmware Over the Air, and is a method of updating the BLE device's programming (reprogramming it) remotely, rather than by physically connecting it to the computer. 

FOTA works (on the Nordic nRF51822 board), but at the moment we recommend that you don't use it unless you know how to make it secure.

___

##Prototypes and Getting Information From Users

Prototyping is a lot easier (and faster) if you don't have to build an app for user interaction. Not only are apps lots of work, they also aren't compatible with different operating systems (iOS and Android), or even with different versions of the same operating system.

So if you're in the prototyping phase, there are three easier ways to allow user interaction:

1. Hardware inputs directly to the BLE device, for example a [touchscreen](http://developer.mbed.org/components/cat/touchscreen/).

2. Websites that provide a standard user interface and send commands back to the device. They require programming, but they usually work well on all phones.

3. [Evothings Studio](http://evothings.com/getting-started-with-evothings-studio-in-90-seconds/) lets you create simple apps that are run from the Evothings App on your phone, so Evothings does the compatibility work for you. It requires some learning of its own, but it may well be worth your time.

Once your prototype is approved, you can invest some more time in your user input. At this point, apps may become worthwhile. But, if you want to be part of the Physical Web, stick to a website - and use the BLE device just to advertise the site's URL.

<a name="internetaccess">
##How a BLE Device Gets Internet Access
</a>

At the moment, BLE devices don't have independent internet access. To get internet access, you can do one of three things:

1. You can give your board a secondary communication method, like Ethernet or WiFi. This can easily double the price of the board, however. 

2. The BLE device can get internet over its BLE connection to a mobile phone. When the phone terminates the BLE connection, the BLE device will lose its internet access. This doesn't require additional hardware, so it doesn't affect the price of the board, but it does mean that for the device to have constant internet access it will need a phone (or BLE-enabled computer) next to it.

3. In the future, we may find routers that accept BLE connections, in the same way that they currently accept WiFi connections.
______

<a name="ble_in_depth"/>
##BLE in Depth
</a>

It's time to look a little bit more at how BLE actually works, and especially at how you can use advertising and services for different purposes.

###Peripheral and Central Devices v Servers and Clients

When we connect devices over BLE, we think of them as being either a peripheral device or a central device. The BLE devices we'll be building here are the peripherals, and the central devices will be our phones or tablet, picking up information transmitted from the peripherals. 

BLE uses two additional terms to describe the connecting entities: server and client. *Server* is the device that has information it wishes to share, and in BLE that is the peripheral. *Client* is the device that wants information and services, and in BLE that is the central device - the phone.

The client controls the connection, in the sense that the server (the BLE device) cannot force the client to scan for BLE devices, view their information, connect or maintain a connection with them and so on. The client is free to establish or terminate a connection and decides for itself how often to ask the server for information. However, the server can recommend some things to the client, and you'll see [later](connection_parameters) how that's done.

###Advertising and Connected Mode

When you set up a BLE device, the first thing it does it advertise its presence (using the Generic Access Profile method, or GAP) - send out a bit of information at a steady rate. This is called *advertisement mode*. The advertisement is what other devices, like your phone, pick up. It tells them that there's a BLE device that wants to talk to them.

Sometimes, all the information you need to send out will fit in an advertisement, so you don't need to do anything else. But sometimes you'll want to provide more information or a service, and for that you'll need to set up a "conversation" between your BLE device and a user's phone. This conversation is what's known as *connected mode*, and it describes a relationship between two devices - the peripheral BLE device and the central device.

Advertising and Connected modes cannot co-exist; a BLE peripheral device (like a heart rate monitor) can only be connected to one central device (such as your mobile phone). The moment the connection is established, the BLE peripheral device will stop advertising, and no other central device will be able to connect to it (since they can't discover that the device is there if it's not advertising). New connections can be established only after the original connection is terminated and the BLE peripheral starts advertising again.

###Services and Profiles (GATT)

*Services* are the method that two BLE devices use to transfer information between them in connected mode (never in advertising mode). Services use the Generic Attribute Profile (GATT) to structure the information according to characteristics, and they're bundled together in various profiles. We'll explore characteristics in more detail below. 

*Profile* may sound like a big concept, but it's simply a way of ensuring that services are combined correctly, as sometimes more than one service is needed to get a device working. For example, the Heart Rate *profile* includes two services: the Heart Rate service and the Device Information service. The Blood Pressure profile similarly includes the Blood Pressure and Device Information services.

BLE has been around for a while, so it has some standard services that you can tap into. Going back to our heart rate monitor example, the heart rate service is well established and very easy to use; it can read information from a BLE heart rate monitor and send it to an app. You'll see that in a later [coding sample](#heartratesample).

Before you start working on a project, it's worthwhile to see if there's already a service that can do what you need done; it'll save you lots of coding and testing. You can find the list of available profiles and services [here](https://developer.bluetooth.org/TechnologyOverview/Pages/Profiles.aspx).

###Characteristics and Interactions

Services break their data down into *characteristics*. Each characteristic is mapped onto a single data point - it tells you one thing, and one thing only. For example, the [Device Information service](https://developer.bluetooth.org/TechnologyOverview/Pages/DIS.aspx) has the following characteristics:

* Manufacturer name.

* Model number.

* Serial number.

* Hardware revision.

* Firmware revision.

* Software revision.

* System ID.

* IEEE 11073-20601 regulatory certification data list.

Each of these characteristics should only contain the information its label says it contains. Together, they reveal the device's manufacturer information and make up a full Device Information service, which as we saw is itself bundled into quite a few profiles.

Characteristics can be either static (like your device's manufacturer name) or dynamic: your device can generate a new value for them as required. For example, in the Heart Rate service, the current heart rate is a characteristic that gets a new value regularly.

Some characteristics are two-way entities: the server (the BLE peripheral) can send them, but it can also receive new values for them from the client (the phone/tablet). This two-way traffic is how BLE becomes interactive - the user sends a new value to one or more characteristics and the device responds to these new values. For example, in the Heart Rate service, the *Heart Rate Control Point* characteristic allow the client to write to it; changing the value of the characteristic tells the device to re-start the Energy Expended measurement.

However, the client doesn't decide which characteristics can be modified; the service states, for each characteristic, whether or not clients have permission to write to that characteristic. In our example, the service has stated that the client has permission to write to the Heart Rate Control Point characteristic. If it revoked the permission, the user would not be able to reset the Energy Expended measurement, because the Heart Rate Control Point would never accept a new value.

<a name="connection_parameters"/>
##Connection Parameters
</a>

There are several parameters that affect the connection between the central and peripheral devices. You'll see later how to edit them. For now, we'll just explain a few of them:

####Connection Interval

The connection interval suggests to the central device how often to check the peripheral for new data. Note that the central device can reject the suggestion and use whichever interval suits its needs; the peripheral cannot enforce the suggestion, because that might overload the central device's communication infrastructure.

The connection interval has two parameters: *MIN_CONN_INTERVAL* (for the shortest interval) and *MAX_CONN_INTERVAL* (for the longest interval). The two together define the range of intervals. Note that the value they receive is in milliseconds. For example, the following code means that the shortest interval time is 250 milliseconds, and the longest is 350 millisecond:

	#define MIN_CONN_INTERVAL 250
	#define MAX_CONN_INTERVAL 350

**Tip:** Although the central device can ignore your suggestions, you should always put some thought into them. For example, if your temperature sensor takes a reading every second, the connection interval shouldn't be much smaller than that, as it will not get new information on most requests; you should offer a connection interval that matches the rate at which you expect to generate new data.

####Connection Supervisory Timeout

Sometimes, devices move out of each other's transmission range, or lose the connection for some other reason. The devices don't know if the connection was lost, but they can assume it was if enough time has gone by without receiving any information from the other side. This is called timeout. The Connection Supervisory Timeout parameter defines the time to wait for a data transfer before assuming that the connection was lost.

The parameter is called CONN_SUP_TIMEOUT, and receives a value in milliseconds. For example, the following code means that the timeout is six seconds:

	#define CONN_SUP_TIMEOUT 6000

####Slave Latency

We said earlier that the client (the phone) asks the server (the BLE device) for information. But, sometimes the client may ask the server for new information when the server doesn't have any new information to send. For example, the client may ask for a new temperature reading, but the temperature sensor may not have provided any new readings for the BLE device to send.

Ideally, when the BLE device is not receiving any information, it would like to sleep - not process information or respond to connection events - to save its battery. If it answers every connection event from the client, it will be forced to work when it could have been sleeping. 

The device can therefore be told to ignore a certain number of data requests that are generated while it has no new data to send. This means that the device can continue sleeping, despite the client's attempt to ask for information.

The parameter is called SLAVE_LATENCY, and receive a value of number of connection events (requests from the client) to ignore. For example, the following code means that the device can ignore four connection events:

	#define SLAVE_LATENCY 4

The difference between SLAVE_LATENCY and MIN_CONN_INTERVAL is that MIN_CONN_INTERVAL is used even when there is new data to send, while SLAVE_LATENCY is used only when the BLE device has no data.

<a name="limitations"/>
###What Can't you Do?
</a>

Technology always has limitations. For BLE, the most important ones are:

1. The BLE device can talk only to phones, tablets etc. It doesn't yet support meshing, which is direct communication between BLE devices.

2. As we explained [earlier](#internetaccess), the BLE device doesn't have independent access to the internet. It requires either additional hardware or constant access to a BLE-enabled device with its own internet access, such as a mobile phone.

3. For BLE to truly be low-energy, it has to work as little as possible. That means, for example, limiting the frequency of its broadcasts, letting it sleep whenever there is no new data to handle, etc. We'll look at these parameters in other sections, such as the [discussion about connection parameters](#connection_parameters) and some of our coding samples.

4. Bluetooth signals have a limited range, with Class 2 devices limited to about ten meters (33 feet); these can be extended with an antenna. Signals can be blocked by concrete and metal, so they don't always travel through walls. 

5. Bluetooth 4 doesn't work on older mobile phones, but as phones are upgraded quite often, in a year or two you can expect the majority of phones in the west to be able to communicate with our devices.

______

<a name="uribeaconsample"/>
#Sample: URI Beacon (and an Intro to the mbed Compiler)
</a>

**Note:** To complete tutorials, you'll need an account on [mbed.org](https://developer.mbed.org/account/signup/?next=%2F). 

We're starting with the URI Beacon because it's a quick, simple way to get a BLE device going. URI Beacons send a bit of information (usually a URL) to any nearby device.  They're really easy to set up, because the code is fully available on the mbed website, so all you'll need to do is tell the beacon what to broadcast. 

##What You'll Need

To get this going, you'll need:

+ To see BLE devices and their advertisement or beacon information, get *one* of the following installed on your phone: 

	-  The physical web app. You can get that app for [iOS](https://itunes.apple.com/us/app/physical-web/id927653608?mt=8) and for [Android](https://play.google.com/store/apps/details?id=physical_web.org.physicalweb).

	- For Android, you can get [nRF Master Control Panel](https://play.google.com/store/apps/details?id=no.nordicsemi.android.mcp&hl=en).

	- For iPhone, you can get [LightBlue](https://itunes.apple.com/gb/app/lightblue-bluetooth-low-energy/id557428110?mt=8).

+ A BLE-enabled mbed board, but don't worry if you don't have one yet - we'll show you how it would have worked.

+ A user on [developer.mbed.org](developer.mbed.org) to see the compiler. We recommend you get the compiler even if you don't have a board yet, so that you can play along with the example.

##Quick Guide

If your'e familiar with mbed and our compiler, you can get the beacon working in just a few minutes:

1. Open the compiler and select or add your board.

2. Import the [BLE_URIBeacon](http://developer.mbed.org/teams/Bluetooth-Low-Energy/code/BLE_URIBeacon/) program.

3. In main.cpp, find the line *nrfURIBeaconConfigService uriBeaconConfig(ble, **"http://www.mbed.org"**);* and edit the URL. Note that it's limited to 30 characters, with http:// and www. each counting as one.

5. Compile the code. It will be downloaded to your Downloads folder.

6. Drag & drop the compiled file to your board.

7. On the app you installed on your phone, discover your beacon and check that the URL is correct.

##Getting Started With the Compiler

The mbed Compiler can take the same program and compile it to match any mbed board. This means you're not constrained in your board selection, but it also means that you need to tell the compiler which board you're working with at any given time.

To select a board for the program: 

1. Log in to mbed [site](https://developer.mbed.org) with your mbed account.

2. Plug your board into your computer's USB port. The board will be displayed in your file browser as a removable storage (similar to plugging in your phone or a USB stick).

3. In your file browser, double-click the board to see its files. By default, every board has an HTML file. 

4. Double click the board's file to navigate to its page on the mbed site. 

5. On the board's page, click *Add to your mbed Compiler*.

6. The compiler will open with your board. You're ready to program. 

##Getting a URI Beacon Program

URI Beacons have a basic structure that's fully available on the mbed website. All you need to do is import it to the compiler and replace the default information with your own. To do that:

1. Go to the [BLE_URIBeacon](http://developer.mbed.org/teams/Bluetooth-Low-Energy/code/BLE_URIBeacon/) page.

2. On the right-hand side of the page, click *Import this program*.

3. The compiler will open with an import dialog box. You can give your program a name, or use the default (BLE_URIBeacon),

4. Click *Import*. The program will be imported for the board you selected in the previous section. 

You can now edit the beacon. We'll show you below how to do it, but first we'd like to explain the program a little. You can skip 
[ahead](#edituribeacon) if you feel like you're not quite ready for C++ yet.

___

##Understanding the Code

**If you don't want to get too deeply into the code - skip [ahead](#edituribeacon).**

The URI Beacon program is a very small and simple one. The only part of it that you need to look at is the *main.cpp* file, which is - as the name suggests - the program's main file. The other files you can ignore - they're there to help the compiler do its job.

Click *main.cpp* to see its code.

###Comments

The first thing you'll see is a bunch of green text, sitting between /* a  * /. This text is comment text, meaning the complier doesn't read it - it's intended for humans. Any text you see between /* and */ is always comment, and some might help you understand the code.

###Including Other Files

	#include "mbed.h"
	#include "BLEDevice.h"
	#include "nrfURIBeaconConfigService.h"
	#include "DFUService.h"
	#include "DeviceInformationService.h"

The next bit of the program is the inclusions list. This tells the compiler which files other than the main.cpp file it needs to include when it compiles your program. You can see that the URI Beacon program has five files it includes. These all focus on different capabilities, such as working with the mbed board (mbed.h) or the BLE itself (BLEDevice.h).

###Objects

You may have heard the phrase "object oriented programming". It's a big concept, but it's easy to understand (in a simplified way) using an analogy. If you think of houses as an object type, it's easy to understand that *your* house is an instance, or occurrence, of that type of object. Your house has a blueprint that was used to construct it, and a set of characteristics such as number of rooms and colour of window frames. You can use the same blueprint to create many houses, and they'll all be separate instances of the same object type. 

Once you've created instances you can use each one independently of the others. So you could, for example, create a hundred houses and then re-paint the window frames on just one of them. Manipulating the object or using the object to affect others is done using functions. It's important to understand that if you have the definition of an object, but don't have an instance of the object (in other words, if you only have a blueprint, but haven't actually built the house) you can't get anything done with your house; you cannot hang up pictures before you've built the walls.

In our program, we have an object type called BLEDevice. This is a blueprint that includes instructions for communicating with the BLE API (remember that the BLE API is a way of telling the BLE chip what to do without need to know how it does it). The first line of our program builds an instance of the object - builds an actual house - and gives it a name. We do this by first saying what we want to build, and then what to call it. So the line

	BLEDevice ble;

Says "give me an instance of the object type BLEDevice, and call it ble", so now we have an object that knows how to talk to the BLE API.

There's a lot more code in the program, but we'll ignore it for now. You'll learn about it in later samples. Let's just see how to set up the beacon to advertise what we want it to.

___

<a name="edituribeacon"/>
##Editing the URI Beacon
</a>

URI Beacons are used to send a URL (a website's address). The line of code in our program that does that is:

	nrfURIBeaconConfigService uriBeaconConfig(ble, "http://www.mbed.org");

You can very easily spot the interesting bit - it's "http://www.mbed.org". You can replace that URL with a URL of your choosing (but make sure to leave the quotes and the *http://www.* bit).

The URI Beacon isn't limitless in size. It can only accept 30 characters, with HTTP:// counting as one, and WWW. counting as another one. If your URL is very long, you'll have to use services like [bit.ly](https://bitly.com) and [tinyurl.com](http://tinyurl.com) to get a short version.

##Compiling and Installing Your Program

For your code to work on a board, it needs to be compiled: the compiler takes all of the files it needs and turns them into a single file, in our case HEX. That file can then be installed on your board. 

To compile and install your program:

1. In the compiler, click *Compile*.

2. The compiled code is automatically sent to your *Downloads* folder as a single file of type HEX.

3. If you've unplugged your board from the USB port, please re-plug it now.

4. Drag & drop the HEX file to the board's entry in the file browser.

5. As part of the installation process, the board is disconnected and reconnected. 

6. Your board is now working as a URI beacon with the URL you gave it. If it has a battery, you can unplug it from the computer and walk around with it.

##Finding Your URI Beacon

Using one of the applications you installed on your phone during our *What You'll Need* section, discover your beacon and check that the URL is correct.

Congratulations! You've created your first BLE device.
 
##Recap: the URI Beacon

To get a URI Beacon:

1. You gave your phone the ability to discover BLE devices using a BLE application. 

2. You imported your board to the mbed Compiler, so that the compiler knows which board to prepare your code for.

3. You imported the URI Beacon program from mbed.org to your compiler.

4. You edited the program to include your own URL. 

5. You compiled and installed the program on your board, so that the board's BLE chip broadcast your beacon.

6. You used your phone to find the beacon broadcast by your board.

7. You had a nice cup of tea to celebrate. 

Along the way, you also learned a little about object oriented programming and the general principle of importing, compiling and installing programs. 

**Tip:** You don't have to send a URL with the beacon. You could send a very simple text (remember that it can't exceed thirty characters, and don't forget to put it in quotes). For example, you could replace the URL with "Now open on Sundays!", just to let your shoppers know about your new hours.

_____

<a name="heartratesample"/>
#Sample: Heart Rate Monitor (BLE Services)
</a>

**Note:** To complete tutorials, you'll need an account on [mbed.org](https://developer.mbed.org/account/signup/?next=%2F). 

The heart rate service gathers the heart rate reading from a monitor and sends it to an app in a profile that's been standardised for that purpose. That means that if you want to work with a heart rate monitor, you don't have to write your own code just to get the input from the device to your phone.

##What You'll Need

If you don't already know how to import your board and a program into the compiler, please see the [URI Beacon](#uribeaconsample) sample.

1. If you haven't already done so, import your board to your compiler. 

2. Import the [heart rate service](http://developer.mbed.org/teams/Bluetooth-Low-Energy/code/BLE_HeartRate/) program to your compiler. 

3. To see the heart rate information on your phone, download PanoBike for [iOS](https://itunes.apple.com/gb/app/panobike/id567403997?mt=8) or [Android](https://play.google.com/store/apps/details?id=com.topeak.panobike&hl=en).

##Quick Guide

If your'e familiar with mbed and our compiler, you can get the heart rate monitor working in just a few minutes:

1. Open the compiler and select or add your board.

2. Import the [heart rate service](http://developer.mbed.org/teams/Bluetooth-Low-Energy/code/BLE_HeartRate/).

3. In main.cpp, find the line *const static char     DEVICE_NAME[]        = **"Nordic_HRM"**;* and change the beacon's name from Nordic_HRM. 

4. Compile the code. It will be downloaded to your Downloads folder.

5. Drag & drop the compiled file to your board.

6. On the PanoBike application, watch the heart rate. It should go form 100 to 175 in increments of one, then reset.
____

##Understanding the Heart Rate Service

**If you don't want to get too deeply into the code - skip [ahead](#renamebeacon).**

The Heart Rate Service forms part of the Heart Rate Profile (together with the Device Information Service). It connects a heart rate monitor to an app that requires its input, for example a fitness app.

The service has [three characteristics](https://developer.bluetooth.org/TechnologyOverview/Pages/HRS.aspx):

* **Heart Rate Measurement** - sends the heart rate to the app.

* **Body Sensor Location** - describes where on the body to put the sensor.

* **Heart Rate Control Point** - receives a value from the user when the user wants to reset the *Energy Expanded* measurement.

##Understanding the Code

The code we generated for this sample may seem long and complex, but when we break it down to components, it becomes clear that the heart rate portion is quite simple.

###Setting Up the Service (Creating an Instance of the Object)

We start with setting up the service:

    /* Setup primary service. */
    uint8_t hrmCounter = 100;
    HeartRateService hrService(ble, hrmCounter, HeartRateService::LOCATION_FINGER);

The first line is only a comment, telling us the general purpose of this section. 

The second line sets up a fake heart rate for the purpose of this sample:

    uint8_t hrmCounter = 100;

It's a parameter that we call hrmCounter, and we give it an initial value of 100 (in the context we'll be using it, it means 100 heart bits per minute). Because we're programming in C++, we used *uint8_t* to indicate to the compiler that the parameter hrmCounter is of a type called unsigned integer, and its length is 8 bits. We won't get into what that means now, but there's plenty of information on line if you're interested in parameter types.

The third line of code is more interesting, as in it we set up the full service. Let's take a closer look at it:

    HeartRateService hrService(ble, hrmCounter, HeartRateService::LOCATION_FINGER);

In our [URI Beacon](#uribeaconsample) sample we talked about objects and their instances. To get the heart rate measurement we want, we need to create an instance of an object called HeartRateService. This is an object that's defined as part of BLE_API, so you can find its .h file in your compiler by going to **BLE_HeartRate > BLE_API > services > HeartRateService.h**.

When we create the instance of the object, we first give it a name (in this case *hrService*), and then provide it with information it requires to be set up correctly:

1. **ble** - this is a reference to the fact that we're using a BLE device. 

2. **hrmCounter** - the initial value of the counter; we defined this as 100 in the previous line.

3. **HeartRateService::LOCATION_FINGER** - where on the body to attach the sensor. The HeartRateService.h has a list of locations, and we've selected the finger.

**Tip:** The information an object requires to be initialised correctly is part of the overall definition of the object, and in this case can be found in the HeartRateService.h file.

###Using the Service (While and If loops)

####Objects and Functions

Once we create an instance of the object by giving it a name and its initial parameters, we can start using it. Object have functions that are defined along with them (they're part of the object's blueprint), and can be accessed from every instance of an object. In this case, the functions are all in the HeartRateService.h file that we used to create the object.

This is what we do with the hrService object:

	while (true) {
        if (triggerSensorPolling && ble.getGapState().connected) {
            triggerSensorPolling = false;

            /* Do blocking calls or whatever is necessary for sensor polling. */
            /* In our case, we simply update the dummy HRM measurement. */
            hrmCounter++;
            if (hrmCounter == 175) {
                hrmCounter = 100;
            }

            hrService.updateHeartRate(hrmCounter);
        } else {
            ble.waitForEvent();
        }

Let's break that down.

####While

Before saying what the program should do (the function), we tell it when to do it. We've created a WHILE loop that will keep going so long as the condition it's checking returns the value TRUE. For the function to stop running, then, the condition it's checking will have to become false.

The condition we're checking for this loop has two parts:

	if (triggerSensorPolling && ble.getGapState().connected)

1. **triggerSensorPolling:** do we have a sensor that's relying data to the BLE device?

2. **ble.getGapState().connected:** do we have a GAP connection between our peripheral device and a central device, and is our peripheral device advertising? This condition has two parts of its own, which are not defined here - they're defined in a function called *getGapState*, which returns a status for the GAP connection. If the function returns the status *connected*, we consider this part of the condition to be met.

Both parts of the condition must be true for the condition as a whole to be considered true. In other words, the loop will not run if we're not getting information from the sensor, or if the GAP status is not "connected".

####Manipulating Parameters - Increments

While the loop is running, it updates the heart rate reading it sends our fitness app. Since we're faking a sensor, our code supplies fake values:

	hrmCounter++;

C++ has several shorthands it uses for common mathematical actions. When we see *hrmCounter++*, it means that hrmCounter's value grows by 1. It's the same as saying hrmCounter = hrmCounter + 1. This is called an *increment operator*.

In our code, every time the loop runs we take the current value of hrmCounter (it starts at 100, because that's the value we gave it when we set up our service earlier), and add 1. So our app will show 100, 101, 102, 103...

####If

But we don't want the heart rate to grow indefinitely, so we created a condition:

            if (hrmCounter == 175) {
                hrmCounter = 100;
            }
            hrService.updateHeartRate(hrmCounter);

This condition is checked every time the loop runs: every time we're done adding 1 to our heart rate, we check its new value. When it reaches 175, we change it to 100 and start counting to 175 again. 

Note that we use two equal signs (==) to check the condition, not one. This is because we're checking if hrmCounter equals 175, not giving it the value 175. If we were to write *hrmCounter = 175*, we'd be assigning the value to the parameter. We did that earlier in the code, when we gave the parameter its initial value of 100, and we do it again in the very next line, when we once again assign 100 as its value.

Note also that the IF is nested in the WHILE loop; it doesn't wait for the WHILE loop to finish running, but rather runs as part of it.

####Updating Objects

When we determine what the heart rate is (our incremented value or back to 100), we set that as the value of the heart rate in the service. We called our instance of the service *hrService* earlier, so that's what we call it now. As an object of type HeartRateService, it has a function called updateHeartRate (defined in the HeartRateService.h file), and that function can accept as an input our hrmCounter. So, let's say the current value of hrmCounter is 83. We say:

            hrService.updateHeartRate(hrmCounter);

Which means, in plain English, "tell the object *hrService* to use its function *updateHeartRate*; that function will update the object's heart rate value to *hrmCounter's* value".

####Waiting for Events

The last bit of the WHILE loop is the ELSE section. ELSE tells the program what to do if the condition of the WHILE loop isn't met. Remember that our condition was to have a sensor that's providing information and an active GAP connection. If the program sees that we don't have one or the other of these, it will enter the ELSE clause. 

            ble.waitForEvent();

When we created our object we said that it's a BLE device, and that gave it the ability to use the function waitForEvent that belongs to the BLE. waitForEvent lets the device sleep until something is needed of it, to reduce battery usage. When an event occurs, for example when the heart rate monitor starts sending values (which is a condition of the WHILE loop), the device will wake up and update the value in the service. 

##Recap: the Heart Rate Service

To summarise, this is how we used the Heart Rate service:

1. BLE_API gives us a .h file called HeartRateService, which holds all the code we need to correctly set up a service object.

2. In our main.cpp file, we created an object of type HearRateService, and called it hrService.

3. To correctly initialise the object, we gave it three parameters, one of which is an initial heart rate value. We called the parameter holding that value hrmCounter and gave it the value 100.

4. Before using the object, we defined when we want to use it: whenever there is a sensor giving us information, and a GAP connection between the BLE device and a client.

5. Then we created a heart rate value to give the object. In a normal service, this value will be provided by the heart rate sensor. Because we're not using a sensor, we created a fake value that is a one-step increment from the previous value. We reset the value to 100 every time it reaches 175.

6. When we have our value, we update the service by using the object's built-in update function: hrService.updateHeartRate(hrmCounter).

7. Lastly, we said that if we can't meet the conditions set up in step #4, we'll let the device sleep until it receives an event, at which point it will check the condition again. 

___

<a name="renamebeacon"/>
##Renaming Your Beacon
</a>

Your device's name is part of the advertisement information, and you can (and should) change it from a standard name to something you'll easily recognise. 

To rename your beacon, find the following line of code:

	const static char     DEVICE_NAME[]        = "Nordic_HRM";

The default name is "Nordic_HRM". You can change it to anything you like (but stay under thirty characters). Don't forget to leave it in quotes. 

	const static char     DEVICE_NAME[]        = "I_Renamed_This";

**Tip**: iOS "sticks" to the name it first discovers for each beacon, so whatever name you choose now you'll have for a while. This is called *cacheing*, and is intended to save your phone some time and energy. 

___

#WAITING FOR SAMPLE TO BE READY, DON'T BOTHER READING

<a name="ledservice"/>
#Sample: Setting Up a Service
</a>

##Creating a Service

Although BLE has many existing services, you might want to create your own service. At this point, there's no real way to get around knowing C++, but if you know how to program, creating a new service is quite simple. 

###The Long Version

[Nordic](https://www.nordicsemi.com/eng/nordic/download_resource/24020/2/80193304) published a guide to programming for BLE that includes service creation information, as well as more detailed explanations of BLE mechanics. 

###The Short Version

To get a service:

1. Give it a 128-bit UUID (16-bit UUIDs are reserved for official services). Find a UUID generator that fits your OS or try a [web-based one](https://www.uuidgenerator.net).

2. 

#Text to remove!
