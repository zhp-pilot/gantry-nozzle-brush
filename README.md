# Gantry mounted nozzle brush for V2 and Trident TAP users.

![Gantry Nozzle Scrubber_small](https://user-images.githubusercontent.com/128906443/227751284-758225bf-d4f5-4e49-b0c3-dafe351a7f91.png)

## CREDITS

This is an adaptation of the Decontaminator Nozzle Scrubber by [edwardyeeks]( https://mods.vorondesign.com/detail/eiGz71BOprk2GapXbQVgA). The mount is derived from the fixed Klicky mount by [jlas1]( https://github.com/jlas1/Klicky-Probe).

## DISCLAIMER 

***THIS MOD IS INTENDED FOR ADVANCED USERS ONLY AND WILL REQUIRE SETTING UP YOUR PRINTER WITH VERY TIGHT TOLERANCES, LIKELY REQUIRING MODIFYING YOUR Y-MAX AND ADJUSTING YOUR PHYSICAL BED LOCATION IF YOU WANT TO RETAIN THE FULL XY BUILD AREA OF YOUR PRINTER. READ THIS WRITE UP AND THE PROVIDED CONFIG FILE IN THEIR ENTIRITY BEFORE PROCEEDING. YOU ARE USING THIS MOD AT YOU OWN RISK AND THE AUTHOR ASSUMES NO LIABILTY FOR ANY DAMAGE RESULTING FROM THE USE OF IT.***

## PURPOSE
This mod is intended for users of TAP to provide a safe nozzle cleaning routine that can be performed at the end of print. With the original Nozzle Scrubber mod, the Z has to lower to the brush, risking crashing the toolhead into printed parts if performed at the end of a print. With this mod, the scrubbing can be performed at any height as the brush is mounted to the gantry. There are no Z movements in the provided config, as such, the cleaning will be performed at the current height when the macro is called.

**This mod is NOT recommended for Klicky, Euclid, or any variant that has a probe dock mounted on the rear gantry extrusion.** The intent is for this mount to be installed where the probe mount would typically be installed on the far left. Trying to use this mod in conjunction with another gantry mounted mod, one risks the movements of the two interfering with each other and potentially causing damage. There are NO safety parameters is the macro to check if the movements are safe and won't collide with other objects.

## IMPORTANT INFO
On a 2.4, the gantry mount needs to be installed so that it clears the bed extrusions. On a standard bed install, the mount will hit the extrusion during homing, QGL, and bed mesh operations, and maybe even when the nozzle is at 1-2 mm or below. Remember with TAP, the gantry actually keeps moving down after the nozzle hits the bed.  I don’t have a Trident to test on, but I assume the same would hold true for the rear bed mount extrusion.

The standard gantry mount has an overall height of 80mm and a depth of 72mm (excluding the brush holder). The mount is height adjustable by 3mm via slotted holes. If you find these dimensions do not work for you, the Fusion360 file is parametric. There are two User Parameters, one for height and one for depth, that you can change to easily update the model. If you are unfamiliar with parameters in Fusion360, click on the Modify drop down and select Change Parameters at the bottom. To change the dimension, click on the value in the Expression column.

It's a tight fit installing this and will require some testing/adjustments on your behalf. My current setup is probably the worst-case scenario at this point for the amount of space needed for Stealthburner/CW2 and CW2-mount mods. With TAP you lose ~3mm of real estate over the standard X-carriage. I also have the Enclosed Orbiter 2.0 mod, and with this, the Stealthburner cowling is pushed out another 1mm or so. Additionally, I'm using hartk's mod to relocate the Y-endstop to the A-motor mount which also limits how far back the X-gantry will go. On my 350 build, I have my Y-max set at 355. The back of the bed is at 350, which is approximately 2mm off the brush measured from the nylon body of the brush as it sticks out slightly. I have 3mm foam on my doors and with the toolhead at X0, there's about 2mm of space between the cowling and door. This will limit the hotend fan so be aware of that and don't leave your toolhead parked at X0 heated for an extended amount of time. The only time mine is there is for a few seconds for the purge line. Also, the type and location of your Y-endstop can also affect your useable space. I removed the lever on the switch which allowed the X-carriage to go back another 1mm or so. **Play around with the setup and see what works. Make sure you manually move the toolhead around and check for clearances. If you feel it won’t fit and you still want to use this mod, then you may need to limit your printable Y dimension (e.g. set your Y-max at 350 and update you slicer bed profile to have a Y-dimension of 345). YMMV.**

Since the mount will be so close to the bed, having rear stops for your build sheet is highly recommended. I’ve included an STL of a slightly modified version from the original Purge Bucket and Nozzle Scrubber mod. This uses M3 SCHC instead of the M2 self-tappers in the original. Use M3x8 SHCS and place the stops on the bed mount extrusions in direct contact with your bed. Please pay attention to these over time. Since they in direct contact with bed they can be prone to warping and the screws start leaning back. Also, if you aren’t careful putting the build sheet on you can break these. **Be very careful and check these regularly. Print some extras at the beginning to have some backups.**

## PARTS REQUIRED
- Brass or nylon brush ([Amazon](https://www.amazon.com/gp/product/B08P4DSTCM/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1) or [AliExpress](https://www.aliexpress.com/item/33053117369.html?spm=2114.12010615.8148356.2.315e106dfzI86U))
- 2x M3 brass threaded inserts (Voron spec)
- 2x M3x12 or M3x16 SHCS
- 2x M5x10 BHCS and 2x M5 T-nuts
- 4x M3x8 SHCS and 2x M3 T-nuts (for rear bed stops)

## ASSEMBLY
### GANTRY NOZZLE BRUSH
- Install M3 brass threaded inserts into the gantry mount.
- Install the brush holder on the gantry mount with either M3x12 SHCS or M3X16 SHCS.
- Install modified brush into the brush holder. See edwardyeeks mod [here]( https://mods.vorondesign.com/detail/eiGz71BOprk2GapXbQVgA) for more information if you aren’t familiar with this.
- Install mount to the rear gantry extrusion using M5x10 BHCS.
- Setup config file following the directions in the file.

### BED STOPS
- Install M3x8 SHCS into top holes a few mm. These are installing into plastic so be careful.
- Install the stops to the bed mount extrusions using M3x8 SHCS. Make sure they are in contact with the bed.
- Adjust the top M3 screws as needed so they are just proud of your bed/magnet. Just high enough you can reference your build sheet on while installing.
- Carefully look at the installed build sheet and confirm it's flush with the back of the bed. Any overhang reduces the clearance you have for the brush. 

## ADDITIONAL INFO
I use this mod as part of the print_end macro. It's important to have an adequate retract to limit oozing after the nozzle is cleaned. I turn the heaters off early and added a 15 sec wait command before calling the clean_nozzle macro. This allows any oozing that's going to happen to occur before the clean. You'll have to experiment with this to find what works best for you.

Example:
```
[gcode_macro PRINT_END]
gcode:    
    # safe anti-stringing move coords
    {% set th = printer.toolhead %}
    {% set x_safe = th.position.x + 20 * (1 if th.axis_maximum.x - th.position.x > 20 else -1) %}
    {% set y_safe = th.position.y + 20 * (1 if th.axis_maximum.y - th.position.y > 20 else -1) %}
    {% set z_safe = [th.position.z + 2, th.axis_maximum.z]|min %}
    SAVE_GCODE_STATE NAME=STATE_PRINT_END
    M400                    ; wait for buffer to clear
    TURN_OFF_HEATERS        ; turn off bed and extruder heaters
    G92 E0                  ; zero the extruder
    G1 E-2.0 F2000          ; retract filament
    G90                     ; absolute positioning
    G0 X{x_safe} Y{y_safe} Z{z_safe} F10000  ; move nozzle to remove stringing
    G1 E-10.0 F5000         ; retract filament more
    G0 X{th.axis_maximum.x//2} Y{th.axis_maximum.y - 2} F3600  ; park nozzle at rear
    G4 P15000               ; wait 15 secs for nozzle to start cooling
    STATUS_CLEANING         ; set LEDs to cleaning
    CLEAN_NOZZLE            ; clean nozzle on brush
    M107                    ; turn off part cooling fan
    BED_MESH_CLEAR          ; clear bed mesh
    STATUS_READY            ; set LEDs to ready
    RESTORE_GCODE_STATE NAME=STATE_PRINT_END
 ```
