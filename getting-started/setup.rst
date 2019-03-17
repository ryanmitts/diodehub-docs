################################
Setup
################################

Install Firmware
==================

:ref:`esp-installation`

Hookup Your Lights
====================

Hookup your power supply to the light strip.

Connection pin 12 of your ESP device to the data line of the light strip.

Make sure the ground of the power supply is connected with the controller.

Get a ClientId and ClientSecret
================================

These are what your device will use to authenticate with the DiodeHub servers.

You will set this up at `DiodeHub <https://diodehub.com>`_.

Setup ESP
==============

When the ESP first boots, it will enter setup mode.

You can connect to it directly using your phone or computers WiFi.

The SSID will be prefixed with ``DiodeHub-``.

Once connected, if your device does not automatically take you to the configration portal, you may browser to ``192.168.4.1``.

Enter the required information about your setup.

Control Your Lights!
======================

You can use the `DiodeHub <https://diodehub.com>`_ website, or the API documented in these docs.
