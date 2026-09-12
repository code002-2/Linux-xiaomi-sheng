# Installation guide (dual-boot)

[中文](../安装指南.md) | **English**

Follow these steps exactly.

## Prerequisites

- The device bootloader is unlocked
- The device currently runs Android only (no other Linux partition)

## Preparing the files

1. Get the rootfs and boot images: from the build repository of your distribution (see the "Supported distributions" table in the repository README), or from this repository's Releases.
   Use the boot image and rootfs whose names contain `single` for single-boot, and the rootfs with `dual` for dual-boot.
2. Get `parted`: use the copy bundled in TWRP, or install it from your distribution's packages.
   (This repository no longer ships the binary.)

---

## Installation steps

### 1. Boot into TWRP

```bash
adb reboot recovery
```

### 2. Push the parted binary

```bash
adb push <path/to/parted> /sdcard
```

### 3. Open an adb shell

```bash
adb shell
```

### 4. Create the Linux partition

```bash
chmod +x /sdcard/parted
/sdcard/parted /dev/block/sda
```

Inside parted, run:

```bash
print          # list partitions and note the userdata number (leftmost, e.g. 29)
rm 29          # delete the userdata partition

# Create the new partitions (example: 256 GB total, 128 GB userdata + 128 GB linux)
mkpart userdata ext4 12.7GB 140.7GB
mkpart linux ext4 140.7GB -0MB

#1T: 512G each
mkpart userdata ext4 12.7GB 524.7GB
mkpart linux ext4 524.7GB -0MB

#512G: 256G each
mkpart userdata ext4 12.7GB 262.35GB
mkpart linux ext4 262.35GB -0MB

print          # verify the new layout: 29 = userdata, 30 = linux
quit
```

### 5. Exit the shell and reboot to the bootloader

```bash
exit
adb reboot bootloader
```

### 6. Flash the images

```bash
fastboot erase dtbo_b
fastboot flash boot_b boot-*.img
fastboot flash linux rootfs-*.img
fastboot set_active b
fastboot reboot
```

### 7. Expand the filesystem after the first boot

Once Linux has booted, expand the filesystem to the full partition size:

```bash
sudo resize2fs /dev/sda30
```

Note: the default rootfs image is only 8 GB, so it must be expanded manually.

---

## Single-boot

Only the Debian single-boot image is currently provided.

### 1. Flash the images

```bash
fastboot erase dtbo_ab
fastboot flash boot （the boot image you downloaded）
fastboot flash userdata （the rootfs you downloaded）
fastboot reboot
```

### 2. Expand the filesystem after the first boot

Once Linux has booted, expand the filesystem to the full partition size:

```bash
sudo resize2fs /dev/sda29
```

Note: the default rootfs image is only 8 GB, so it must be expanded manually.
