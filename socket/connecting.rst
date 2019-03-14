***********
Connecting
***********

Credentials
============
You must have a clientId and clientSecret for a device generated from the DiodeHub console.

Connection Client
==================
I recommend `wscat <https://github.com/websockets/wscat>`_ for testing the API.

Connection URL
===============

``wss://socket.diodehub.com``

Connection Headers
===================

The initial HTTP upgrade request to start communication using web sockets must be authenticated using `HTTP basic authentication <https://tools.ietf.org/html/rfc7617>`_.

Authorization Header Psuedo Code:

``Authorization: Basic base64({clientId}:{clientSecret})``

Connection Example
===================

.. code-block:: bash
    :caption: Using wscat
    :linenos:

    wscat -c wss://socket.diodehub.com --auth abc124:abc-123-abc

Connection Limits
==================

A socket connection can be idle for up to 10 minutes. The maximum connection time is 2 hours.

The health messages discusses in the next section serve to keep the connection open. The client should automatically reconnect when disconnected after the 2 hours.

.. Note:: The socket API does not support the ping/pong socket control frames. Messages are sent using the text opcode.
