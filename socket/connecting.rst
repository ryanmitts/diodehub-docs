***********
Connecting
***********

SSL Certificate
================

The SSL certificate of the socket endpoint is self signed with a private CA certificate.

This is so devices connecting to the endpoint can have the CA cert pinned without needing it changed.

If using a commonly trusted certificate, we would have to make sure the same root CA always signed certificates that the devices are pinned to.

If the root CA changed that signed our certificates, devices would no longer validate requests to the endpoint, and would lose communication to the server.

The private CA certificate we generated to sign the endpoint certificates is valid until 2049. The endpoint certificates are rotated every 2 years.

CA Certificate
--------------------

.. code-block:: text
    :caption: CA cert
    :linenos:

    -----BEGIN CERTIFICATE-----
    MIIDnDCCAoSgAwIBAgIJAIsy+WUsdCVMMA0GCSqGSIb3DQEBCwUAMGMxCzAJBgNV
    BAYTAlVTMQswCQYDVQQIDAJXQTEQMA4GA1UEBwwHU2VhdHRsZTERMA8GA1UECgwI
    RGlvZGVIdWIxIjAgBgkqhkiG9w0BCQEWE3J5YW5taXR0c0BnbWFpbC5jb20wHhcN
    MTkwMzE3MDQzOTExWhcNNDkwMzA5MDQzOTExWjBjMQswCQYDVQQGEwJVUzELMAkG
    A1UECAwCV0ExEDAOBgNVBAcMB1NlYXR0bGUxETAPBgNVBAoMCERpb2RlSHViMSIw
    IAYJKoZIhvcNAQkBFhNyeWFubWl0dHNAZ21haWwuY29tMIIBIjANBgkqhkiG9w0B
    AQEFAAOCAQ8AMIIBCgKCAQEAvx4LvPiUZau4rHRSBnXl8KYp9ZPbU/1upjQftxut
    IDfdM5gEXAZYSgE5DaVIh0iVmSU+Jb6vcDCrXVbbsrvY1sCR4FS2Lb8q23zbcVQO
    xyB6KRctt73f+BEEoYFginjUUdXOY2J8azSIcisQSBFMzrR7ZVSXomQJZqpKzaZm
    4lVINmS3WtnCt6bOYQF/39qjvGMyDF0arerM/LBOAoAfgJ0lRcFAVW0r8h3V3Qq6
    s+G5O+qGe88or8/kQODPKvOneO5QSAivNCEvNotmoWq73YAzsXflzFvoSwhpFEr2
    6oOPq+YqgVeDX6yqUaFxT9ASB7lN4BdRyFsrOAtFNZIJiwIDAQABo1MwUTAdBgNV
    HQ4EFgQUWP9X6NcLU9UAddvVTXF1jjyQUWMwHwYDVR0jBBgwFoAUWP9X6NcLU9UA
    ddvVTXF1jjyQUWMwDwYDVR0TAQH/BAUwAwEB/zANBgkqhkiG9w0BAQsFAAOCAQEA
    Op4CmzsefKIKGBWacQSyr69Y97q/B53FXT7BDSoZ/kAV/SYWiEzEcXhAXDIPrZEg
    +ELQnIyKVJJqVJjKOH5lfoerJ2vot0KwTLbwg+3m8SU4z8K4o2RgY7QQS6QuvDim
    GtlAHLDSPozM7vTFiC9HtQSOo5yAZzzTJZJFVaKOnQrydNixJ5YlCxXc7mnYD42I
    WPa+peEf8u1c7ZlLFgkx8yE++xKsv10zVuEtcRHyASx5nyAJaY2n9Pkn7tDR3Sj+
    2APzoe30pSwgTQ6BJ5CsSKnrRaJNmQLu8GjFNfLKe37qw3Efi0fAo98fA9WVMvsH
    4nzFNNjsUJysBoSwQl3khw==
    -----END CERTIFICATE-----



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

The initial HTTP upgrade request to start communication using WebSockets must be authenticated using `HTTP basic authentication <https://tools.ietf.org/html/rfc7617>`_.

Authorization Header Psuedo Code:

``Authorization: Basic base64({clientId}:{clientSecret})``

Connection Example
===================

.. code-block:: bash
    :caption: Using wscat
    :linenos:

    wscat -n -c wss://socket.diodehub.com --auth abc124:abc-123-abc

Connection Limits
==================

A socket connection can be idle for up to 10 minutes. The maximum connection time is 2 hours.

The health messages discusses in the next section serve to keep the connection open. The client should automatically reconnect when disconnected after the 2 hours.

.. Note:: The socket API does not support the ping/pong socket control frames. Messages are sent using the text opcode.
