# cr-10-v3-marlin-config

My configuration for Marlin 2.x and my CR-10 V3 which is now mostly cosmentic and 1-2 personal tweaks.

Forked from: https://github.com/MarlinFirmware/Configurations/tree/release-2.0.8/config/examples/Creality/CR-10%20V3

When Marlin 2.0.8 was relased I found there was now a CR-10 V3 template maintained by Aaron Just (big thank you to Aaron). Most of the tweaks I was previously applying to the CR-10 V2 template for my firmware are now pre-configured in Aaron's configuration.

I have basically taken all of the remaining differences from my modified V2 configuration and merged them into Aaron's V3 template and/or used Aaron's values instead of mine because I suspect they know what they are doing where I was just guessing.

My original post: https://www.pickysysadmin.ca/2020/08/16/marlin-2-x-for-a-cr-10-v3/

The firmware has X and Y offsets pre-configured in it for the BLTouch based on this mount: [CR-10 V2 BL Touch Mount](https://www.thingiverse.com/thing:3947349)

I did not configure the Z offset in firmware since that might be unique per printer.

# Compiled firmware changes with Marlin 2.0.9.x

The Marlin Firmware developers have gotten a lot more strict around the configuration files. Previously all I had to do was enable or disable BL Touch and things would take care of themselves. This is no longer the case and since I do not need non-BL enabled firmware I am going to stop compiling it instead of figuring out the  configuration changes I would now have to make.

My advice. Get a BL Touch. They cost the same as 1-2 spools of filament and make printing a lot easier.


# Changes/tweaks from stock CR-10 V3 config:

* Set `CUSTOM_MACHINE_NAME` because symantics
* Custom logo/version strings
* Set `HEATER_0_MAXTEMP` to `275` so the maximum temperature of the CR-10 V3 can be reached (260F)
  * Marlin has a built-in saftey where it takes the max temperature, subtracts 15F and then that becomes the max temperature so 275 - 15 = 260
* Set `NOZZLE_TO_PROBE_OFFSET` to match where my BLTouch is (you might need to change this)
* Disabled `RESTORE_LEVELING_AFTER_G28` because I use Gcode to handle all this manually and to make sure my bed leveling offsets aren't loaded when I run a mesh-level
* Disabled `AUTO_REPORT_SD_STATUS` because I'm tired of seeing it in my logs. I know the microSD card isn't installed. I can see. [Issue 6](https://git.pickysysadmin.ca/FiZi/cr-10-v3-marlin-config/-/issues/6)
* Enabled `SERIAL_PORT_2 1` [Issue 2](https://git.pickysysadmin.ca/FiZi/cr-10-v3-marlin-config/-/issues/2)
* Multiple builds of the firmware, one with BLTouch enabled and one with it disabled for those who haven't installed a BLTouch yet
  * BLTouch Enabled, 250000 baud
  * BLTouch Enabled, 115200 baud


# Downloads
Pre-compiled firmware can be found in the [Compiled Firmware](https://git.pickysysadmin.ca/FiZi/cr-10-v3-marlin-config/-/tree/master/Compiled%20Firmwares/) folder or on the [Releases](https://git.pickysysadmin.ca/FiZi/cr-10-v3-marlin-config/-/releases/) page


# Extra info

Post firmware flash I recommend running the following GCode (change the M851 line to match your Z offset):

```
M502; Factory reset your printer
M500; Save settings
M851 Z-2.370; Set Z Probe Offset
M500; Save settings
M501; Load settings
```