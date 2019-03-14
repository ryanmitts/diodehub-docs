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

Inbound Message
================

Light Message
---------------

The control message that instruct the device what light effect to show.

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
