# cr-10-v3-marlin-config

My configuration for Marlin 2.x and my CR-10 V3

Forked from: https://github.com/MarlinFirmware/Configurations/tree/import-2.0.x/config/examples/Creality/CR-10%20V2

My original post: https://www.pickysysadmin.ca/2020/08/16/marlin-2-x-for-a-cr-10-v3/

I have successfully printed using this configuration.

The firmware has X and Y offsets pre-configured in it for the BLTouch based on this mount: [CR-10 V2 BL Touch Mount](https://www.thingiverse.com/thing:3947349)

I did not configure the Z offset in firmware since that might be unique per printer.

I guess some of you use long USB cables that have problems at 250000 baud. I am now also compiling a slower version of the firmware that will run at 115200 for those who need it. I will sort out the firmware naming convention whenever Marlin 2.7.0.3 comes out. For now if the firmware filename does not include "115200b" assume it is the 250000b version. Either way the firmware will work, it just may be slower than you are expecting if you flash the 115200b version instead of the 250000b version.


# Changes/tweaks from stock CR-10 V2 config:

* Enabled `POWER_LOSS_RECOVERY`
* Set `CUSTOM_MACHINE_NAME` to match the CR-10 V3 (instead of V2)
* Custom logo/version strings
* Set `HEATER_0_MAXTEMP` to `275` so the maximum temperature of the CR-10 V3 can be reached (260F)
  * Marlin has a built-in saftey where it takes the max temperature, subtracts 15F and then that becomes the max temperature so 275 - 15 = 260
* Set `DEFAULT_AXIS_STEPS_PER_UNIT` so `E0` is `415` for the Titan Drive
* Set `NOZZLE_TO_PROBE_OFFSET` to match where my BLTouch is (you might need to change this)
* Set `INVERT_E*_DIR` to `TRUE` because the Titan drive is backwards I guess?
* Disabled `RESTORE_LEVELING_AFTER_G28` because I use Gcode to handle all this manually and to make sure my bed leveling offsets aren't loaded when I run a mesh-level
* Multiple builds of the firmware, one with BLTouch enabled and one with it disabled for those who haven't installed a BLTouch yet
  * BLTouch Enabled, 250000 baud
  * BLTouch Disabled, 250000 baud
  * BLTouch Enabled, 115200 baud
  * BLTouch Disabled, 115200 baud




# Downloads
Pre-compiled firmware can be found in the [Compiled Firmware](https://git.pickysysadmin.ca/FiZi/cr-10-v3-marlin-config/-/tree/master/Compiled%20Firmwares/) folder or on the [Releases](https://git.pickysysadmin.ca/FiZi/cr-10-v3-marlin-config/-/releases/) page


# Extra info

Post firmware flash I recommend running the following GCode (change the M851 line to match your Z offset):

```
M502; Factory reset your printer
M500; Save settings
M851 Z-2.380; Set Z Probe Offset
M500; Save settings
M501; Load settings
```

Enjoy!

![Status Screen](/images/status-screen.jpeg)

![Version Screen](/images/version-screen.jpeg)
