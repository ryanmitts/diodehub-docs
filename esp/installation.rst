.. _esp-installation:

*************
Installation
*************

From Binary
====================
If you wish to install the firmware onto an ESP32 device without setting up the entire build environment to do so.

Install ESPTool
-----------------

This is the flashing utility provided by the chip manufacturer, Esprissif, to be able to flash the chips.

The tool is `here <https://github.com/espressif/esptool>`_, and following the "Easy Installation" works well, just make sure you have Python installed first.

You should be able to run ``esptool.py`` from your terminal after installing this.

Download Firmware
-------------------

From the releases page of this repository, download the four ``.bin`` files that need to be flashed onto your chip.

Place these all into one folder.

Get Ready to Flash
--------------------

If you are using the DevKit ESP32, plug the USB cable into your computer and identify the port for which it was assigned. On Windows this will be a ``COMX`` value, and on OSX/Linux it will be ``/dev/ttyUSB0`` or something.

Flash
-------

Run the following command, replacing the portion noted with your port.

.. code-block:: bash
    :caption: Command to flash firmware
    :linenos:

    esptool.py \
    --chip esp32 \
    --port {your port, COM5, /dev/ttyUSB1, etc.} \
    --baud 921600 \
    --before default_reset \
    --after hard_reset \
    write_flash -z \
    --flash_mode dio \
    --flash_freq 40m \
    --flash_size detect \
    0xe000 ota_data_initial.bin \
    0x1000 bootloader.bin \
    0x10000 diodehub-esp.bin \
    0x8000 default.bin

From Source
====================

The project can be built using `ESP-IDF <https://docs.espressif.com/projects/esp-idf/en/stable/get-started/>`_.

[More to come.]