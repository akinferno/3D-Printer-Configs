**DISCLAIMER**: Use at your own risk. I know enough to not be afraid to tinker. And like tinkering so much, I don't mind breaking stuff and fixing it later. That said, I will not intentionally break stuff. All of my changes are commented in the files below, meaning followed by ';' and a comment.


## **ORCASLICER CHANGES**

Next to ‘FLSUN T1 0.4 nozzle’ printer, click the little ‘edit’ icon. Click the ‘Machine G-code’ tab.  Replace what is there with the following:
 

# **Machine start G-code:**
```
G21
G90
M82
G28
M140 S[first_layer_bed_temperature]
M104 S150 T0                         ; Set hotend temp to 150C
M190 S[first_layer_bed_temperature]
G1 Z150 F3000
G1 X-130 Y0 Z0.4
M104 S[first_layer_temperature] T0   ; moved down from the original position between Bed temp changes.
M109 S[first_layer_temperature] T0   ; moved down from the original position between Bed temp changes.
M107 T0
G92 E0
G3 X0 Y-130 I130 J0 Z0.3 E30 F2000
G1 Z2 F2000
G92 E0
{if bottom_solid_infill_flow_ratio == 1}  ; if 1st layer flow ratio is 1 (default)
  M221 S{filament_flow_ratio[0] * 100}  ; Set flow ratio of the filament
{else}
  M221 S{bottom_solid_infill_flow_ratio * 100} ; Or set flow to 1st layer flow ratio
{endif}
TIMELAPSE_TAKE_FRAME  ; Should start the timelapse, this has not been tested.
SET_TMC_CURRENT STEPPER=extruder CURRENT=0.8
```

# **Machine end G-code:**
```
M107 T0
M104 S0
M140 S0
M221 S100  ; Set flow ratio back to 100%
G92 E0
G91
G1 E-2 F2100
G1 Z+0.5 F6000
G28
G90
TIMELAPSE_RENDER   ; Should finalize the timelapse file, also not tested
```
 

# **Layer change G-code:**
```
{if layer_z < total_layer_count}  ; if layer is below top layer
  M221 S{filament_flow_ratio[0] * 100}  ; Set to filament flow ratio
{elsif layer_z == total_layer_count and top_solid_infill_flow_ratio != 1}
  M221 S{top_solid_infill_flow_ratio * 100}  ; If top layer AND flow ratio is NOT 1, change flow rate.
{endif}
TIMELAPSE_TAKE_FRAME ; Should take a new picture for the timelapse, this has not been tested.
```
