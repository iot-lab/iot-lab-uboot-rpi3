### Generate boot.scr

    mkimage -A arm -O linux -T script -C none -n boot.scr -d boot.source boot-sd/boot.scr

### Copy kernel and dtb to tftp

    sudo cp kernel/* /var/iot-lab-rpi/tftp/rpi3/.

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

