# Customized OpenWrt fork based on official OpenWrt 15.05 Chaos Calmer release

_See wnr2200ru branch is you are looking for changes to proper support Netgear WNR2200 routers (mainly for russian and china revisions)._

Customizations and patches applied to vanilla source code at "custom" branch:

## Packages

* 6in4.sh - IPv6-in-IPv4 tunnel backend was updated to support recent changes in Hurricane Electric automatic ipv6 tunnel update.
* relayd package was updated to version 83dba5d525a3b7c2ae4fcb24961143bfcfc93ba7 (2015-10-29) from openwrt trunk

## Procd changes

* Fixes to "tmpfs on zram" feature - added proper options for mkfs.ext4, added proper mount options

## Glibc changes (for glibc builds)

* glibc source revision is updated to newer version
* Added various patches for secuirity fixes, minor performance improvements.
  Added some fixes from openSUSE GNU/Linux distribution.

## Kernel patches and config changes

Patches applied for all kernels, but kernel-config changes now performed only for ar71xx and x86 builds,
other configs are left intact for now. Use "make kernel_menuconfig" to manually enable features that require config updates (UKSM and BFS for now).

* Added UKSM feature (http://kerneldedup.org/projects/uksm/download).
  It helps when using router as simple server (especially when using debian inside LXC). Highly experimental, USE AT YOUR OWN RISK! May be removed in future.
* Added BFS feature (http://ck.kolivas.org/patches/bfs/). Does not help much for ar71xx boads, so it may be removed someday.
* Kernel config changes to enable proper LXC support, enabled FPU emulator for ar71xx boards to support running debian for mips inside LXC container.
* Default tcp congestion control is set to westwood+ (may be changed back to default someday).
* Kernel 3.18 updated to newer patch-version from kernel.org, openwrt specific patches verified and updated.
  090-overlayfs-fallback-to-readonly-when-full.patch applied with fuzz, but it is ok for now (not modified to simplify future merges with vanilla openwrt tree).
* Kernel code that moved to new module dma-buf (DMA shared buffer support) is brought back to be built-in, because this change cause issues in my usecase.

