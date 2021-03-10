---
layout: default
title: G27 - Park toolhead
nav_order: 1
parent: Raccolta Macro di Desuuuu
has_children: false
permalink: /g27/
---

## G27 - Park toolhead
Park the nozzle at a predefined XYZ position.

```
[gcode_macro G27]
default_parameter_X: 20
default_parameter_Y: 290
default_parameter_Z: 20
gcode:
  {% if printer.toolhead.homed_axes != "xyz" %}
    {action_respond_info("Please home XYZ first")}
  {% else %}
    SAVE_GCODE_STATE NAME=G27_state
    G91
    G1 Z{Z}
    G90
    G1 X{X} Y{Y} F3000
    RESTORE_GCODE_STATE NAME=G27_state MOVE=0
  {% endif %}
```
