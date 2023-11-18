# Neptune-4-Pro---My-setup-settings-files
The printer.cfg and PrusaSlicer setup that I use.... "suped up" with many macro additions etc.

There are numerous added Macros for many various tasks/reasons.
When there is a Macro in Klipper, Fluidd will add a button for that Macro, so you can click
on that to run any Macro that is designed for running "stand-alone".  Even Macros that are
NOT intended to be run on their own will still have a button assigned.

The printer.cfg is quite re-organised, into better groups of the categories etc, seeing
Klipper does not care what order things are in, and Elegoo have a hodge podge of what is where.

The Stepper X&Y position_min and position_endstop are changed to negative values that allow
setting X=0 and Y=0 to be just a few millimetres onto the print bed - so that in a Slicer
X=0 Y=0 are the truly minimum values to use.
The max_positions are X=237 Y=233, which allow the Printhead to move to very close to the true
maximum possible positions, and then you set the real limits of the print bed in your Slicer.
So in the Slicer bed settings the two maximums to set are:  X=226  Y=224   which, again, limits
print bed use to be within a few millimetres of those edges.

I use a [Homing Override] section that overrides what G28 would otherwise do. It does much the 
same as usual but moves the Printhead off the far left rear of the bed, for the Cleaning Brush
Wipe - but also for any Purge-Line that you might use instead, or also.

There is a Beeper function set up, plus a M300 G-Code macro to play sounds.

The standard PRINT_START and PRINT_END are blank now.  And a START_PRINT and END_PRINT macro
are added to be used for those functions. This is because you can end up with a 'double'
PRINT_START call in some circumstances of calling htat from your Slicer - that might be an
"Elegoo specific" bug, and not in other Klipper printers(?). So using a different macro name
assures that cannot happen.
START_PRINT includes a call to the added PURGE_WIPE macro, so remove that section if you do
NOT have the Cleaning Brush Mod added.

Many standard macros have been altered and  "improved" over the stock ones.

Macros added:

BED_SCREWS
This runs the screws_tilt_adjust function of Klipper, to calibrate your bed corners. It heats
the bed and then runs the calibration, in that one command.

BED_MESH_60
Heats the bed to 60degC and then runs the bed_mesh_level Klipper function.

Z_OFFSET_CHECK
Homes the printer and moves the Printhead to the middle of the bed, at Z=0.5mm height, so that 
you can then continue with the "paper test" by moving down to Z=0 which is where the paper 
should be gripped fairly firmly. From that Z=0 position, if the paper is not gripped at the
correct pressure, use the Z_Offset controls on the Screen to adjust the Z_Offset - taking note
of the AMOUNT OF CHANGE you had to do, then use that value to adjust the Z_Offset entry that in
the printer.cfg  SAVE_CONFIG section.
A more positive Z_Offset will make the Nozzle come DOWN more for Z=0. So the adjustment amount
you noted gets added, or subracted, according to which way you had moved it (up or down).

PURGE_WIPE
This Macro is mainly called by the START_PRINT Macro, to do the Cleaning Brush Wipe sequence IF
you have that mod added.

LEDS_FRAME_ON   LEDS_FRAME_OFF   LED_NOZZLE_ON   LED_NOZZLE_OFF
These macros replace the stock Elegoo "stupidly names" ones!

Standard MArlin G-Codes supported/added:
G29   Run the Bed Mesh calibration function
M84   Disable Stepper Motors
M109  Heat the Hotend and WAIT for the target temp
M140  Heat both the Inner and Outer Bed Heaters and DO NOT WAIT for that target temp
M141  Heat only the Outer Bed Heater and DO NOT WAIT for that target temp
      Having this command extra allows you to have a way to set/control either Bed Heater
M190  Heat both the Inner and Outer Bed Heaters and WAIT for that target temp
M191  Heat both the Inner and Outer Bed Heaters and WAIT for that target temp
M201  Set Maximum Acceleration limits (only X&Y supported)
M203  Set Maximum Feedrate(s) (velocities) (only X&Y supported)
M204  Set Maximum Acceleration limits (only X&Y supported)
M205  Set Square Corner Velocity - only for X&Y, but only ONE SCV value exists really.
M300  Play a frequency, for chosen time length
M420  Load the Bed Mesh DEFAULT profile




