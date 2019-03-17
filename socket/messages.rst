*********
Messages
*********

The message format is JSON based, and all messages have an action and a data key.

The action key value is the type of message you wish to send, and the data value is the payloads/contents of that message.

.. code-block:: json
    :caption: Generalized JSON schema of the message format
    :linenos:

    {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "properties": {
            "action": {
                "type": "string"
            },
            "data": {
                "type": "object"
            },
            "required": ["action"],
            "additionalProperties": false 
        }
    }

Outbound Messages
==================

These messages are outbound from the device to the socket service.

Ready Message
---------------

Send when your device is ready to accept communication after connecting to the socket server. The server will respond with a light message of the last permanent message the device was displaying.

Your device will likely need to re-connect occasionally, due to gatway timeouts, lost connections, etc. You likely only want to send this message after it powers on, that way the light effect does not reset.

.. code-block:: json
    :caption: Example ready message
    :linenos:

    {
	    "action": "ready"
    }

Health Message
---------------

This message must be sent at least once every 10 minutes from the device to keep the connection open. It also keeps track of some device statistics.

.. code-block:: json
    :caption: Example health message
    :linenos:

    {
        "action": "health",
        "data": {
            "uptime": 100,
            "freeHeap": 123000,
            "version": "0.0.1",
            "md5": "68349344a20093db3070f9199c82e0f6"
        }
    }

.. _socket-inbound-message:

Inbound Messages
================

In bound messages are sent to the device using the DiodeHub website, or directly using the :ref:`socket-api`.

Light Message
---------------

The control message that instruct the device what light effect to show.

The data payloads for light messages can be found in the :ref:`light-effects` section.

.. code-block:: json
    :caption: Example light message
    :linenos:

    {
        "action": "light",
        "data": {
            "effect": "rainbow",
            "options": {
                "subEffect": "rotateRight",
                "speed": 10
            }
        }
    }

Update Message
---------------

The control message that instruct the device that it should perform an OTA update.

The location of in the payload must be a download location of a bin file of the new firmware.

The DiodeHub website will send these messages when you update through the site.

.. code-block:: json
    :caption: Example light message
    :linenos:

    {
        "action": "update",
        "data": {
            "location": "https://diodehub.com/firmware/new.bin",
            "version": "v0.0.1"
        }
    }
