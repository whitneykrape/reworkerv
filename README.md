# ERV Rework

Currently this is a library for an ESP32-S3 to control a Tosot Mini-ERV. There are few ERV options for folks without ducts. Looking to build out a repository that gathers the options noting pluses and minuses along with modifications needed to get each option working. 

Quick note, this is my first ESP32 and low voltage project to recheck my notes as you work. 
I don't have this installed into the wall yet but do have the unit operating nicely. 

Next steps:
* Add a physical button. Home Assistant is great but don't like relying on it for control, preference is for physical in-room controls. (Though is is semi-automatic with the CO<sup>2</sup> sensor.)
* Wire in the native 3? volt LED for notification feedback. Keep the ESP32 LED for red-orange-green CO<sup>2</sup> notification (I think this code does that already.)

Last, hopefully Tosot is cool with this and doesn't try and weirdness to lock down their units. It is fine if these units are non-warrantied of course but this is one of the few, reasonably priced, through wall vent units that does not requite major work (adding ducts, drilling out 8 inch holes, so on.)

## Description

portalqubes on reddit put together an awesome guide for using a Tosot Mini-ERV, SU-AORAKI-ERV, using a 12 volt supply (the fan unit is 12 volt) and a buck converter to run the ESP32 at 5 volts. I slightly modified this to use a 12 volt USB-C Trigger Board. Do your own research for the parts, not happy with list. Will try and make a new, tested, list. 12 volt is an optional spec for USB-C, not all wallworts will provide it. 

* [Tosot Mini-ERV](https://www.amazon.com/TOSOT-Ventilation-Conditioner-Residential-Applications/dp/B0DZCN1MQT)
* [Trigger Board](https://www.adafruit.com/product/5991)
* [12 volt to 5 volt eBay?](https://www.ebay.com/sch/i.html?_nkw=12v+to+5v+buck+converter&_sop=12)
* [SCD40](https://www.adafruit.com/product/5187)
* [Anker USB-C Wall Adapter](https://www.anker.com/products/a2147) (Needs to be 30+ watts for headroom)
* [ESP32-S3](https://www.aliexpress.us/item/3256809551889715.html)

(Trying to avoid Amazon, except for the main unit, but it many not be realistic since decent small electronics parts are hard to find otherwise. I did use Amazon originally.)

## Getting Started

### Installing

* Wiring is the trickest part, also this sort of assumes Home Assistant availability currently, looking to make it optional
* Wiring loom
    * Rough list (wiring image to follow)
    * 12 volt supply (trigger board) to fan and buck converter
        * Note, for me, on the ERV fan supply BLACK is POSITIVE and red is negative for the fan
        * I tried this a couple times and the ESP32 kept shutting down and there was a spark wired the other way
        * That said, nothing seemed to be damaged
    * From the 5 volt buck, wire to the noted pins on the ESP32 board, 5 volt and ground
        * GPIO14 and GPIO13 are for the fan PWM (orange and brown)
        * Also had these backwards, no damage from testing, will note the exact wire to pin colors in the future
    * Ground and 3 volt to the SCD40
        * Pins 10 and 9 are for the Sensor, bus_a
        * These are noted in the code, straightforward
    * The original author is using the LED on the ESP32 for notifications but the LED might work at 3 volt?
        * Here red does seem to be positive and black negative (and didn't work in the reverse)
* Update the room name, device name, wifi, and other values in the .yaml
* Install with your favorite ESP installer

## Help

Mostly straightfoward, other than the wiring, but will add pitfalls in the future. 

## Authors

portalqubes [Original Post](https://www.reddit.com/r/homeassistant/comments/1laprlc/anyone_in_need_of_an_esphome_erv/)

## Version History

* 2026.001
    * Branching to try adding a button and using the in built LED
    * (Resetting version number slightly, not using months)

* 2024.11.0
    * Initial Git Release

## License

This project is licensed under the MIT License

Not AI used in this code currently, may need local AI for further development