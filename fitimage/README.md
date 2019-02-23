## FIT Image notes

- Download zImage, DTB and spi-kw-cs.dtbo locally. zImage and DTB can be found
  in Yocto generated kernel/DTB. SPI overlay is part of raspberrypi firmware
  repo
- Build the image:
  ```
  $ mkimage -f iotlab-fitimage.its iotlab-fitimage.itb
  ```
- Check the image:
  ```
  $ mkimage -l iotlab-fitimage.itb
  ```

## U-BOOT specific changes

- git clone U-boot
- add the following lines in configs/rpi_3_32b_defconfig:
  ```
  CONFIG_FIT=y
  CONFIG_OF_CONTROL=y
  ```
- setup the toolchain (32bits):
```
$ export CROSS_COMPILE=arm-linux-gnueabihf-
```
- configure U-boot for the build and launch the build
```
$ make rpi_3_32b_defconfig
$ make
```
- Copy u-boot.bin on the RPI3 SD card

