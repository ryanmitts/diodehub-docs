***********
Routes
***********

POST /message/{clientId}
=========================

Content type is ``application/json``.

Sends a message to the device.

The post body is identical to that of the WebSocket API inbound payloads to a device. See :ref:`socket-inbound-message`.

.. code-block:: bash
    :caption: Sending a light effect message
    :linenos:

    curl --user {clientId}:{clientSecret} \
      --request POST \
      --data '{"action": "light", "data": {"effect": "rainbow"}}' \
      https://socket-api.diodehub.com/message/{clientId}

.. Note:: If you send a light message through this API, it will not be saved and sent to the device after it re-establishes a new connection. Only the website does this.
