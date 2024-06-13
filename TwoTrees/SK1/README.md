#Current TwoTrees SK1 Config

*** Work in progress. Use at your own risk! ***

Config changes so far:
- Corrected Stepper values to match hardware instead of generic Voron info
- Added minimum extrude temperature to prevent filament grinding below extrusion temperature
- Moved macros to a macro.cfg file
- Updated Unload_Matrial macro
- Added KAMP files (Klipper Adaptive Mesh and Purge)
- Customized the Print_Start (sortof, had to create a whole new macro My_Print_Start instead because Print_Start would run twicefor some reason)
  -- Be aware: this won't won't unless you update the Sliecr gcode with the commands commented out above the My_Print_Start

Hardware changes so far:
- Removed rear toolhead cover along with rear toolhead fan.
- Wired all three chamber fans to Fan 0 and Fan 1. This will likely change once I run a new connector to the toolhead for the hotend fan. Or get an enclosure.
