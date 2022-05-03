# Automating Your Smarthome Without the Cloud

I've loved the idea of a smart home for years. When COVID hit, and I found myself in desperate need of a hobby to stay busy, I decided to dive headfirst into home automation. Soon after I realized how much depending on cloud services sucks, and I resolved to run everything in my home locally, with no dependency on anyone else's computers anywhere else on the internet.

After 18 months, a small fortune, and a few curse words, I ended up with a pretty decent setup. I wrote this conference talk about all of the lessons I'd learned.

## Getting started

The first thing you should do, if you haven't seen it, is check out the presentation. 

The rest of this README is supporting information geared to people that have already seen (or read) the talk.

## Home Assistant pointers

I gloss over a few details in the talk in the interests of time. Here's where I clear up any confusion that might have caused...

### ZWaveJS vs ZWaveJS2MQTT

The slides contain screenshots of a Z-Wave control panel, which I say is from the "Z-Wave JS add-on".

That's a little bit over-simplified. I actually use two extensions:

- **Z-Wave JS** ***integration*** allows HA to access the Z-Wave configuration
- **ZWaveJS2MQTT** ***add-on*** is what provides the advanced UI I show

It's all a bit confusing because ZWaveJS2MQTT can *also* decouple your Z-wave network from HA by using MQTT, but that's optional (and is disabled by default). I have the add-on installed only for the advanced configuration UI.

See [ZWaveJS2MQTT on Github](https://github.com/hassio-addons/addon-zwavejs2mqtt) for more details.

### Blueprints ###

A really neat feature that didn't make it into the talk is the idea of "blueprints", which let you define an automation as a sort of template with placeholders for variables, devices, etc.

You can then instantiate this blueprint one or more times, identifying the inputs for those placeholders, and HA will create the automations automatically behind the scenes.

This is really useful when you use the same patterns over and over again because you can manage the logic centrally, rather than in a bunch of copy/paste/modify automations. 

## Devices I like

### Inovelli ###

I've really liked the switches and bulbs I've purchased from [Inovelli](https://inovelli.com/). Fantastic build quality, tons of features, and a very active community with lots of interaction from the company.

Unfortunately the chip shortage has really hammered their available stock, so switches are hard to find, but once stock is available again I highly recommend their stuff.

### Zooz ###

I've also had decent luck with Zooz products, not counting the occasional need to reset a device that wouldn't pair right away.

- [Z-Wave USB stick](https://www.thesmartesthouse.com/collections/zooz/products/zooz-usb-700-series-z-wave-plus-s2-stick-zst10-700)
- [ZSE-18 Motion Sensor](https://www.thesmartesthouse.com/collections/zooz/products/zooz-z-wave-plus-motion-sensor-zse18-with-magnetic-base-battery-or-usb-power)
- [ZEN32 Scene Controller](https://www.thesmartesthouse.com/collections/zooz/products/zooz-700-series-z-wave-plus-scene-controller-switch-zen32)
- [ZEN74 Toggle Dimmer Switch](https://www.thesmartesthouse.com/collections/zooz/products/zooz-700-series-z-wave-plus-s2-toggle-dimmer-switch-zen74)
- [ZSE42 Water Leak Sensor](https://www.thesmartesthouse.com/collections/zooz/products/zooz-z-wave-plus-700-series-xs-water-leak-sensor-zse42)

### Adafruit ###

I got all of my Raspberry Pi, sensors, and electronics stuff from [Adafruit](https://www.adafruit.com/). Great selection, fast shipping, awesome support and documentation.

### Flio.io ###

The [Flic 2 Starter Kit](https://flic.io/shop/flic2-starter-kit) is a little expensive, but once you have the hub you can add many more buttons to it. I have these buttons all over my house at this point!

## DIY hackjobs ##

### Monitoring dryer current ###

[DigiDryerMon on Github](https://github.com/digiblur/digiDryerMon)

Really easy to set up, if you have a few electrical components laying around.

### SwitchBot control for pedastal fan ###

By default, SwitchBot requires a hub; the "bots" themselves use BLE to communicate with the hub, and the hub handles incoming commands.

I didn't want to run another hub, and I wanted the switchbot to be farther away from HA than BLE would allow. I found this [SwitchBot-MQTT-BLE-ESP32](https://github.com/devWaves/SwitchBot-MQTT-BLE-ESP32) project that implements a MQTT-to-BlueTooth bridge using a cheap ESP32 microcontroller.

Basically, the ESP32 microcontroller listens for MQTT messages and then converts them to BLE messages to the SwitchBot. 

Worked great!

### Cameras ###

I haven't wanted to pay for high-end cameras or to pay for video hosting. I've set up a few different DIY things.

I have some Raspberry Pis running [RPi-Cam-Web-Interface](https://elinux.org/RPi-Cam-Web-Interface) and others running [MotionEye-OS](https://raspberry-valley.azurewebsites.net/MotionEye-OS/). They work OK, but it takes some fiddling.

I have also hacked some cheap Wyze cameras with a [custom firmware](https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks) so that I can store the videos locally, instead of on Wyze servers.

I'd say that my camera setup is the most hacky and least satisfying bit of my system right now; a really good camera setup requires more money, time, and wiring than I have been willing to put in.