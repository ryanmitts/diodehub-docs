********
Rainbow
********

Displays the seven rainbow colors fading into one another in a gradient.

There are three sub effect types that you can use:

1. ``rotateRight``
2. ``rotateLeft``
3. ``flash``

.. Note:: The speed option with the flash subEffect represents how long the off/on periods are.

.. code-block:: json
    :caption: Static
    :linenos:

    {
	    "effect": "rainbow"
    }

.. code-block:: json
    :caption: With optional subeffect
    :linenos:

    {
        "effect": "rainbow",
        "options": {
            "subEffect": "rotateRight",
            "speed": 10
        }
    }
