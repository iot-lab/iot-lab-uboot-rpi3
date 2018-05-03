This project contains information for building required boot files that have
to the SD card of a Raspberry Pi3.

The notes explains how to build the `boot.scr` used by u-boot to automatically
configured and download the kernel from the IoT-LAB infrastructure and how
to generate and copy the minimal boot image on the SD card.

### Generate boot.scr

    mkimage -A arm -O linux -T script -C none -n boot.scr -d boot.source boot-sd/boot.scr

### Prepare SD card

    sudo umount /dev/mmcblk0*
    sudo parted -s /dev/mmcblk0 mklabel msdos mkpart primary fat32 1M 30M
    sudo mkfs.vfat /dev/mmcblk0p1
    sudo mount /dev/mmcblk0p1 /mnt
    sudo cp boot-sd/* /mnt
    sudo umount /mnt

### Create the image (optional)
    
    dd if=/dev/mmcblk0 of=iotlab-rpi3-sd.img bs=4M count=9

### Copy the the image on SD card

    dd if=iotlab-rpi3-sd.img of=/dev/mmcblk0 bs=4M

