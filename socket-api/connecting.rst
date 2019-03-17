***********
Connecting
***********

Credentials
============
You must have a clientId and clientSecret for a device generated from the DiodeHub console.


URL
===============

``https://socket-api.diodehub.com``

Authentication
===================

All requests are authenticated using `HTTP basic authentication <https://tools.ietf.org/html/rfc7617>`_.

Authorization Header Psuedo Code:

``Authorization: Basic base64({clientId}:{clientSecret})``
