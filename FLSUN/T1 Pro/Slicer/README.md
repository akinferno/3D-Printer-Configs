**DISCLAIMER**: Use at your own risk. I know enough to not be afraid to tinker. And like tinkering so much, I don't mind breaking stuff and fixing it later. That said, I will not intentionally break stuff. All of my changes are commented in the files below, meaning followed by ';' and a comment.


# **ORCASLICER CHANGES**

- Stopped hotend from heating first. I set it to initally heat to 150C while bed is heating up, then move to purge position, then heat to first layer hotend temp before purging.
- Orca has a setting for top and bottom layer flow. It defaults to '1' in the print settings. This annoys me, so I evaluate to see if it is 1, if so, I use the filament flow rate. If it is not '1', I use the custom value for flow.
- I included this on the layer changes also. If not the last layer, extrusion rate is set to filament flow rate. If it is the last layer and top layer flow dows not equal 1, it uses the custom value, otherwise it uses the filament flow rate. 

Next to ‘FLSUN T1 0.4 nozzle’ printer, click the little ‘edit’ icon. Click the ‘Machine G-code’ tab.  Replace what is there with the following:
 

## **Machine start G-code:**
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
; TIMELAPSE_TAKE_FRAME  ; This doesn't work, I left it here, commented out until I figure out the proper command.
SET_TMC_CURRENT STEPPER=extruder CURRENT=0.8
```

## **Machine end G-code:**
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
 

## **Layer change G-code:**
```
;TIMELAPSE_TAKE_FRAME ; This doesn't work, I left it here, commented out until I figure out the proper command.
```
