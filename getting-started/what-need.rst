################################
What You Need
################################

Light Strip
=============

You will need a WS2812B light strip. I buy mine off Amazon if I need just one, or off Alibaba or Aliexpress if ordering more than one and can wait weeks.

I only have ever used the WS2812B light strips since they seem to be the easiest to get a hold of and use. Since I am using the `FastLED <https://github.com/FastLED/FastLED>`_ library to drive the lights, I'm sure this firmware could be modified to control other light sets too.

I have the LED color buffer set to hold up to 2096 LEDs worth of colors to drive, but I have not hooked up this many lights. I don't think driving this many would be reasonable in this setup as the time to write out that many lights would likely make most effects too slow to be enjoyable, and the amount of power that would consume you would need to have multiple power supplies along the light run. Driving multiple strings at once independently would probably be more feasible, but I have not tried that.

Power Supply
==============

You must have an adequate 5V power supply to power the light set. The WS2812B addressable lights use RGB 5050 LED modules. Each color (RGB) can draw at full power 20mA. Thus each light on full brightness would draw 60mA. If you had a 4 meter strip of 240 lights, this would mean the potential current draw is 14.4A. Much higher than most household 5V power supplies I have seen are able to provide.

I find the full brightness to be extremely bright and unnecessary for my usual use, so I have set lights to only output at half brightness in the FastLED library. This allows you to specify your RGB colors in the usual 0-255 range, and have the brightness automatically scale as the control signals for the lights are generated.

The human high does not perceive brightness linearly, so I find this change not very noticeable and can reduce my current draw by about half. Granted, this is if the lights are displaying solid white -- at half brightness as described, and displaying the rotating rainbow effect, my 240 light strip appears to draw 4.5A roughly from the supply.

So I bought a 10A 5v power supply for my use case. Just please keep this in mind if adjusting the brightness and you have a large light strip.

Most of the supplied that meet these specs look something like `this <https://www.amazon.com/Aiposen-Transformer-Security-Computer-Project/dp/B01B1QKLR8/ref=sr_1_2_sspa?crid=35EZ0OVPPORZS&keywords=5v+10a+power+supply&qid=1551851169&s=gateway&sprefix=5v+10a%2Caps%2C194&sr=8-2-spons&psc=1>`_. You have to hookup an AC power cord yourself and run the wire output of your lights to the output terminals.

ESP32 Module
===============

You will need an ESP32 module on which you can flash the firmware to operate the light strip.

I use and have been developing with the `ESP32-DevKitC V4 <https://docs.espressif.com/projects/esp-idf/en/latest/get-started/get-started-devkitc.html>`_. I buy mine from `Mouser <https://www.mouser.com/>`_ as they are only $10 each, but you have to pay for shipping, or you can buy them on Amazon.

I'm sure other development boards for the ESP32 that you can find will also work. I soon will have a WROOVER one to test on as well.

I am also working to make my own PCB with the ESP32 module to have this run on too. The draft schematics and Gerber files are in this repository.
