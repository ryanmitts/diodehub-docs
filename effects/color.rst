********
Color
********

Displays as many colors as passed.

The amount of lights in your strip is divided by the color amount to determine how many LEDs of each color should be.

.. code-block:: json
    :caption: Static with three colors
    :linenos:

    {
        "effect": "color",
        "colors": [
            "#ff0000",
            "#00ff00",
            "#0000ff"
        ]
    }

.. code-block:: json
    :caption: With optional subeffect
    :linenos:

    {
        "effect": "color",
        "options": {
            "subEffect": "flash",
            "speed": 1000
        },
        "colors": [
            "#ff0000",
            "#00ff00",
            "#0000ff"
        ]
    }
