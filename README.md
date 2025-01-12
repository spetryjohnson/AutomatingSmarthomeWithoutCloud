# Home Automation Without The Cloud

I've loved the idea of a smart home for years. When COVID hit, and I found myself in desperate need of a hobby to stay busy, I decided to dive headfirst into home automation. Soon after I realized how much depending on cloud services sucks, and I resolved to run everything in my home locally, with no dependency on anyone else's computers anywhere else on the internet.

A few months, a small fortune, and a lot of curse words later, I ended up with a pretty decent setup. I wrote this conference talk about all of the lessons I'd learned.

## Getting started

The first thing you should do, if you haven't seen it, is check out the presentation. 

The rest of this README is supporting information geared to people that have already seen (or read) the talk.

## Devices that I like

### Inovelli ###

I've really liked the switches and bulbs I've purchased from [Inovelli](https://inovelli.com/). Fantastic build quality, tons of features, and a very active community with lots of interaction from the company.

### Zooz ###

I've also had decent luck with Zooz products, not counting the occasional need to reset a device that wouldn't pair right away.

- [Z-Wave USB stick](https://www.thesmartesthouse.com/collections/zooz/products/zooz-usb-700-series-z-wave-plus-s2-stick-zst10-700)
- [ZSE-18 Motion Sensor](https://www.thesmartesthouse.com/collections/zooz/products/zooz-z-wave-plus-motion-sensor-zse18-with-magnetic-base-battery-or-usb-power)
- [ZEN32 Scene Controller](https://www.thesmartesthouse.com/collections/zooz/products/zooz-700-series-z-wave-plus-scene-controller-switch-zen32)
- [ZEN74 Toggle Dimmer Switch](https://www.thesmartesthouse.com/collections/zooz/products/zooz-700-series-z-wave-plus-s2-toggle-dimmer-switch-zen74)
- [ZSE42 Water Leak Sensor](https://www.thesmartesthouse.com/collections/zooz/products/zooz-z-wave-plus-700-series-xs-water-leak-sensor-zse42)

### Flic.io ###

I'm a big fan of physical triggers for automations, and the [Flic 2 Starter Kit](https://flic.io/shop/flic2-starter-kit) makes it easy. Each button is about the size of a quarter, sticks to surfaces with adhesive, and lasts for months on a coin battery. 

You can wire up events to a single press, double press, and press-and-hold, and one of the events you can trigger is an API call.

I have mine making webhook API calls into Home Assistant, which then trigger automations to turn on lights, fans, etc. 

### ESP32 microcontrollers ###

The [ESPHome Project](https://esphome.io/) has come a long way recently, and it's never been easier or cheaper to connect electronic components like sensors and IR transmitters to Home Assistant.

This is really where a locally controlled smarthome shines, and you become able to automate things that would literally be impossible any other way.

### AtomS3 Lite ###

The [M5 AtomS3 Lite](https://docs.m5stack.com/en/core/AtomS3%20Lite) is one of the ESP32 boards I use a lot. It has an on-board button and RGB LED, which makes it a great for implementing the "kill switches" I talk about; the LED can indicate whether an automation is enabled or not, and clicking the button can toggle it.

### NSPanel Pro ###

My control panel is a [NSPanel Pro](https://www.thesmarthomebook.com/2022/11/17/home-assistant-on-the-nspanel-pro/) installed in a 2-gang wall switch by my front door.

The switches I replaced were controlling lights, so I just wired those lights to be always-on and put smart bulbs in them. This made room for the panel, and I can still control the lights through Home Assistant.

### Adafruit ###

I got all of my Raspberry Pi, sensors, and electronics stuff from [Adafruit](https://www.adafruit.com/). Great selection, fast shipping, awesome support and documentation.

## Presence Detection ##

Many of my automations need to know which rooms are occupied and which are not.

There are a few different ways to do this:

- **Motion sensors** are great at detecting when people walk into a room, but not great at detecting if people are sitting still
- **mmWave sensors** are super sensitive and can detect micro movements, such as a person breathing, but can suffer from false positives
- **Bluetooth beacons** track a device's distance from a Bluetooth transmitter by monitoring the signal strength, but don't work if people don't carry their phones on their person at all times

I currently use these things in combination with each other, but it's still a work in progress. 

I originally used [ESPresence](https://espresense.com/) for BLE beacon tracking and it was pretty solid, but it required dedicating an entire ESP32 to presence detection.  They aren't terribly expensive, but there are a few places where I would have liked to have been able to add another sensor or something to that device.

I'm currently experimenting with [Bermuda](https://github.com/agittins/bermuda) which uses the BLE Proxy component of ESPHome for tracking, which allows you to add other sensors and components through ESPHome as well.

## Local voice control ##

Voice control has come a long way since I started using Home Assistant.

It's still not ready for prime time use, but it's getting close.

- [$13 voice assistant](https://www.home-assistant.io/voice_control/thirteen-usd-voice-remote/)
- [DIY voice assistant with Respeaker Lite](https://smarthomecircle.com/local-voice-assistant-with-seeed-studio-respeaker-lite)
- [ESP32-S3-BOX voice assistant](https://www.home-assistant.io/voice_control/s3_box_voice_assistant/)
- [Home Assistant Voice Preview Edition](https://www.home-assistant.io/voice-pe/)

## DIY hackjobs ##

### Monitoring dryer current ###

[DigiDryerMon on Github](https://github.com/digiblur/digiDryerMon)

Really easy to set up, if you have a few electrical components laying around.

### Fan controllers ###

I have a number of different IR-controlled fans that I wanted to automate. I've done this by using ESP32 microcontrollers and ESPHome. 

Each controller includes:

* A light sensor or camera to read the fan's current state (on/off, power level, etc)
* IR transmitter to send commands
* 3D printed enclosure so it looks a _little_ less like a bomb stuck to my fan

One of those projects (the one with a camera) I published to Github: [Pureflow Fan Monitor](https://github.com/spetryjohnson/pureflow_fan_monitor)


### Cameras ###

I've tried using Raspberry Pi cameras with [RPi-Cam-Web-Interface](https://elinux.org/RPi-Cam-Web-Interface) and I've also hacked some cheap Wyze cameras with a [custom firmware](https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks) so that I can store the videos locally, instead of on Wyze servers.

Both of those solutions _work_, but they require a bit of fiddling. 

Ultimately, I've been way more satisfied with the [Amcrest IP camera](https://www.amazon.com/Amcrest-5-Megapixel-NightVision-Weatherproof-IP5M-T1179EW-28MM/dp/B083G9KT4C?th=1) that I installed using PoE. You're going to pay more money for cameras that don't use cloud services, but this one has been solid.