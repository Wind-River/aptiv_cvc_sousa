# aptiv_cvc_sousa

This repository contains U-Boot image, U-Boot source code and U-Boot patches for Aptiv CVC Sousa board.

## u-boot-aptiv_cvc_sousa.s32-sdcard

The file `u-boot-aptiv_cvc_sousa.s32-sdcard` is a disk image.
dd command can be used for low-level copying the data of this file to the SD card device as below:

```
$ sudo dd if=./u-boot-aptiv_cvc_sousa.s32-sdcard of=/dev/sd<partition> bs=1M && sync
```

## u-boot-aptiv-cvc-sousa.tar.gz

The file u-boot-aptiv-cvc-sousa.tar.gz is the U-Boot source code.
It's based on NXP Auto Linux BSP(auto_yocto_bsp) release/bsp29.0 with patches meta-uboot-patches-aptiv-cvc-sousa added.

## meta-uboot-patches-aptiv-cvc-sousa.tar.gz

The file meta-uboot-patches-aptiv-cvc-sousa.tar.gz is a Yocto layer used to patch U-Boot. You can use it to rebuild U-Boot.
To rebuild U-Boot you need to have `repo` installed on Linux and its prerequisites.

**Running the below command would be enough to completely build U-Boot to be deployed.**

```
$ mkdir fsl-auto-yocto-bsp

$ tar -xvf meta-uboot-patches-aptiv-cvc-sousa.tar.gz -C fsl-auto-yocto-bsp

$ cd fsl-auto-yocto-bsp

$ repo init -u https://source.codeaurora.org/external/autobsps32/auto_yocto_bsp -b release/bsp29.0

$ repo sync

$ ./sources/meta-alb/scripts/host-prepare.sh

$ source nxp-setup-alb.sh -m s32g274aevb

$ bitbake-layers add-layer ../meta-uboot-patches-aptiv-cvc-sousa

$ bitbake u-boot
```

The built image can be found in `build_s32g274aevb/tmp/deploy/images/s32g274aevb`.

The file `u-boot-sdcard-2020.04-r0.s32` is the produced U-Boot image. It can be renamed to `u-boot-aptiv_cvc_sousa.s32-sdcard`.
