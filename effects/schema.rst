*************
JSON Schema
*************

This is the wholistic schema for all possible light effect payloads.

.. code-block:: json
    :caption: JSON Schema
    :linenos:

    {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "definitions": {
            "speed": {
                "type": "number",
                "minimum": 0,
                "default": 0
            },
            "color": {
                "type": "string",
                "pattern": "^#[0-9A-Fa-f]{2,6}$"
            },
            "baseEffectOptions": {
                "type": "object",
                "properties": {
                    "subEffect": {
                        "enum": [
                            "rotateLeft",
                            "rotateRight",
                            "flash"
                        ],
                        "type": "string"
                    },
                    "speed": {
                        "$ref": "#/definitions/speed"
                    }
                },
                "required": ["subEffect", "speed"],
                "additionalProperties": false
            },
            "meteorOptions": {
                "type": "object",
                "properties": {
                    "meteorSize": {
                        "type": "number",
                        "minimum": 0,
                        "default": 10
                    },
                    "meteorTailDecay": {
                        "type": "number",
                        "minimum": 0,
                        "default": 64
                    },
                    "speed": {
                        "allOf": [
                            { "$ref": "#/definitions/speed" },
                            { "default": 20 }
                        ]
                    }
                },
                "additionalProperties": false
            },
            "fireOptions": {
                "type": "object",
                "properties": {
                    "cooling": {
                        "type": "number",
                        "minimum": 0,
                        "default": 50
                    },
                    "sparking": {
                        "type": "number",
                        "minimum": 0,
                        "default": 120
                    },
                    "speed": {
                        "allOf": [
                            { "$ref": "#/definitions/speed" },
                            { "default": 20 }
                        ]
                    }
                },
                "additionalProperties": false
            },
            "speedOnlyOptions": {
                "type": "object",
                "properties": {
                    "speed": {
                        "allOf": [
                            { "$ref": "#/definitions/speed" },
                            { "default": 100 }
                        ]
                    }
                },
                "additionalProperties": false
            }
        },
        "type": "object",
        "properties": {
            "effect": {
                "enum": [
                    "off",
                    "color",
                    "fire",
                    "meteor",
                    "pulseInOut",
                    "rainbow",
                    "randomTwinkle",
                    "runningColor",
                    "twinkle"
                ],
                "type": "string"
            }
        },
        "allOf": [{
                "if": {
                    "properties": {
                        "effect": {
                            "enum": [
                                "color",
                                "rainbow"
                            ]
                        }
                    }
                },
                "then": {
                    "properties": {
                        "options": {
                            "$ref": "#/definitions/baseEffectOptions"
                        }
                    }
                }
            },
            {
                "if": {
                    "properties": {
                        "effect": {
                            "const": "fire"
                        }
                    }
                },
                "then": {
                    "properties": {
                        "options": {
                            "$ref": "#/definitions/fireOptions"
                        }
                    }
                }
            },
            {
                "if": {
                    "properties": {
                        "effect": {
                            "const": "meteor"
                        }
                    }
                },
                "then": {
                    "properties": {
                        "options": {
                            "$ref": "#/definitions/meteorOptions"
                        }
                    }
                }
            },
            {
                "if": {
                    "properties": {
                        "effect": {
                            "enum": [
                                "pulseInOut",
                                "randomTwinkle",
                                "twinkle",
                                "runningColor"
                            ]
                        }
                    }
                },
                "then": {
                    "properties": {
                        "options": {
                            "$ref": "#/definitions/speedOnlyOptions"
                        }
                    }
                }
            },
            {
                "if": {
                    "properties": {
                        "effect": {
                            "enum": [
                                "color",
                                "meteor",
                                "pulseInOut",
                                "twinkle",
                                "runningColor"
                            ]
                        }
                    }
                },
                "then": {
                    "properties": {
                        "colors": {
                            "type": "array",
                            "items": {
                                "$ref": "#/definitions/color"
                            },
                            "minItems": 1
                        }
                    },
                    "required": ["colors"]
                }
            }
        ]
    }
