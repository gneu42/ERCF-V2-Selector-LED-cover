# **This explain how to set up the LOGO , Staus and Cover LEDs.**

##In your printer.cfg file, add :
```
   [include cover_leds_macros.cfg]
```

##In /config/mmu/base/mmu_macro_vars.cfg change the following variables 
````
[gcode_macro _MMU_STATE_VARS]
description: Happy Hare configuration for state change hooks
gcode: # Leave empty
 # You can extend functionality to all Happy Hare state change macros by
 # adding a command (or call to your gcode macro). E.g for additional
 # LED logic
 variable_user_action_changed_extension      : "_MMU_ACTION_CHANGED_COVER"    ; Executed after default logic with duplicate params
 variable_user_print_state_changed_extension : "_MMU_PRINT_STATE_CHANGED_COVER"    ; Executed after default logic with duplicate params
 variable_user_gate_map_changed_extension    : ""    ;Executed after default logic with duplicate params
 ````



**This is my personnal config as example, you must make the changes needed to match your setup :**

I have the barf led in the gearbox, 13 exit leds, no entry leds, 7 leds for the cover bar graph, 2 leds for the cover carrot logo.
    I have the following chain : 
  * From the RGB connector on the ERB board 
  * => Gearbox Barf (1-8) 
  * => Exit range (9-21) 
  * => status_index (22) 
  * => cover leds (23-29) 
  * => cover logo leafs (30) 
  * => cover logo carrot (31)

## In /config/mmu/base/mmu_hardware.cfg modify the neopixel mmu_leds according your setup.
```
[neopixel mmu_leds]
pin: mmu:MMU_NEOPIXEL
chain_count: 31              # Number gates x1 or x2 + 1 (if you want status)
color_order: GRB, GRB, GRB, GRB, GRB, GRB, GRB, GRB, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW, GRBW        # Set based on your particular neopixel specification

[mmu_leds]
num_gates: 13
led_strip: neopixel:mmu_leds
exit_range: 9-21   
#entry_range: 14-{mmu_num_leds}
status_index: 22   
frame_rate: 24
```


