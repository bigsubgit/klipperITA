---
layout: default
title: G29 - Bed Leveling
nav_order: 2
parent: Raccolta Macro di Desuuuu
grand_parent: Esempi di Macro su Klipper
has_children: false
permalink: /g29/
---

## G29 - Bed Leveling

```
[gcode_macro G29]
default_parameter_T: 0
gcode:
  {% if printer.idle_timeout.state == "Printing" %}
    {action_respond_info("This command cannot be used while printing")}
  {% elif printer.toolhead.homed_axes != "xyz" %}
    {action_respond_info("Please home XYZ first")}
  {% else %}
    SAVE_GCODE_STATE NAME=G29_state
    G90
    G1 Z10 F240
    {% if T|int > 30 %}
      M190 S{T}
    {% endif %}
    BED_MESH_CALIBRATE
    {% if 'S' in params %}
      M140 S{S}
    {% endif %}
    G90
    G1 Z10 F240
    G1 X150 Y155 F6000
    RESTORE_GCODE_STATE NAME=G29_state MOVE=0
  {% endif %}
```
