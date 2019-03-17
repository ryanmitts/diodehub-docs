Welcome to DiodeHub!
====================================

DiodeHub is a project I started to control WS2812B light strips.

Originally, I was using an Arduino to control the lights, but repprogramming the Arduino each time I wanted the lights to change was inconvenient.

I tried controlling the lights using an ESP8266, but the hardware limitations, mainly it's low RAM and it being single core meant that I could not setup SSL and have the lights driven smoothly.

I have since moved on to using the ESP32 chip.

I made a infrastructure, APIs and website I can use to control my lights.

Table of Contents
------------------

.. toctree::

    getting-started/index
    esp/index
    socket/index
    socket-api/index
    effects/index
