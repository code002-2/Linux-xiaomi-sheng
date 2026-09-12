# Switching between operating systems

[中文](../切换操作系统.md) | **English**

## Method 1: GUI tool (requires root)

Switching is done with WoaManager, a tool by @游侠侠 on Coolapk — [download](https://wwl.lanzouq.com/b00eew9kbc) (password: `youx`), [original post](https://www.coolapk1s.com/feed/57455997).

**Android → Linux**

Grant the app root access and open it, then tap "切换到 linux" (switch to Linux). It lists the boot partition to flash and the dtbo partition to erase, and detects them automatically; if detection fails, tap "读取分区" (read partitions) under "分区管理".

Enter the absolute path of the Linux system's dual-boot.img in the "linux boot 路径" field.
(You can long-press the boot file in MT Manager, tap Properties, then long-press the name or directory to copy its full path.)

Save the path, then tap "一键切换" (one-tap switch): the tool flashes boot, erases dtbo and reboots into Linux.

**Linux → Android**

Make sure you are running Android, open the tool, and tap "推送 linux 切换工具" (push the Linux switching tool). It lists the boot and dtbo partitions to back up and the Linux partition to push to.

Before pushing, mount the Linux partition: tap "挂载分区", select the Linux partition under "新增挂载分区" and save. The default mount point is `/data/mounted/linux`; then tap "挂载" to mount it.

Tap "一键推送工具" to push boot, dtbo and the switching script (`.sh`) into the `WoaManager` folder in the Linux root directory. The app will remind you to run that `.sh` file with root privileges.

On the Linux side, run the switching script:

```bash
sudo /WoaManager/android.sh
```

It flashes Android's boot and dtbo images and reboots into Android.

## Method 2: Boot slot switching

Requires bootloader (fastboot) mode and another computer.

**Android → Linux**

```bash
fastboot set_active b
fastboot reboot
```

**Linux → Android**

```bash
fastboot set_active a
fastboot reboot
```
