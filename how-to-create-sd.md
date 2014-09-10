SD Card Creation
----------------

Replace sdX in the following instructions with the device name for the SD card as it appears on your computer.

Start fdisk to partition the SD card:

`fdisk /dev/sdX`

At the fdisk prompt, create the new partitions:

Type `o`. This will clear out any partitions on the drive.
Type `p` to list partitions. There should be no partitions left.
Type `n`, then `p` for primary, `1` for the first partition on the drive, and `enter` twice to accept the default starting and ending sectors.
Write the partition table and exit by typing `w`.

Create and mount the ext4 filesystem:

```
mkfs.ext4 /dev/sdX1`
mkdir root`
mount /dev/sdX1 root
```

Extract the root filesystem (as root, not via sudo):

`tar -xvf /path/to/rootfs.tar.gz -C root`

Flash the bootloader files:

```
cd root/boot
./sd_fusing.sh /dev/sdX
cd ../..
```

Unmount the partition:

`umount root`

Insert the SD card into the board, connect ethernet, and apply 5V power. Default user details are root/root and odroid/odroid.
