# OpenWrt fork based on official OpenWrt 15.05 Chaos Calmer release.

This branch contains customizations needed for NETGEAR WNR2200 - Russian (and maybe Chinese) revisions.
No other changes from "custom" branch is applied here.

See https://wiki.openwrt.org/toh/hwdata/netgear/netgear_wnr2200_v3 and https://wiki.openwrt.org/toh/netgear/wnr2200 for more info.

## Fixes, applied to vanilla branch:

* USB and GPIO fixes. Adopted from this unofficial firmware : http://openwrt.muessigb.net/Netgear_WNR2200/Chaos_Calmer_Builds/150504-b/ar71xx .
  Proper support for hardware buttons is still not complete (I have no time for this), but seems it's possible to make it work. Maybe i'll do this in the future.
* LEDS fixes - it is now possible to use all leds. LAN and WAN leds have two independend color-modes that can be used simultaneously.
* MTD Flash Layout changes in image makefile to support full 16 MiB device size, and use proper location for ART partition.

**Do not try to flash generated image to 8 MiB router version (US and EU revisions).
It will completely overwrite and destroy wifi calibration data inside ART partotion and prevent wifi module to start
If you want to compile image for 8 MiB router revision - compare this branch with vanilla - and manually revert changes at target/linux/ar71xx/image/Makefile**
