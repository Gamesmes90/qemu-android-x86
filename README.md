# qemu-android-x86
This is a modified version of https://aur.archlinux.org/packages/qemu-android-x86

**Using [android-x86-7.1-r5.i686.rpm](https://osdn.net/dl/android-x86/android-x86-7.1-r5.i686.rpm) by default**

Features:
- Easy install any Android version
- libhoudini support (arm64, arm) **guaranteed with android 7.1 32-bit only**
- Read + Write system
- ADB connection out of the box (```adb connect localhost:47000```)

Please take a look at the [configuration](config) file before starting the machine for the first time.

## Change android system
You can change the source file downloaded by editing [PKGBUILD](PKGBUILD) source and [.SRCINFO](.SRCINFO), or simply add a local file. If you chose to use a local file remember that the rpm package must be in the same directory as the PKBUILD file.

Remember to copy the sha256sum

```bash
sha256sum local_package.rpm
```

### [PKGBUILD](PKGBUILD)
```
source=("local_package.rpm::URL"
    ...
    )
sha256sums=('SUM'
    ...
    ')
```
###  [.SRCINFO](.SRCINFO)
```
source = local_package.rpm::URL
sha256sums = SUM
```

#### Note
Keep the order source/sha256sum.

## Read/Write Filesystem
From [this comment](https://aur.archlinux.org/packages/qemu-android-x86#comment-806749) on the same aur repository:

To remount the filesystem as read/write run
```bash
mount -o rw,remount /system
```

Use initrd to automatically remount the filesystem as read/write
- run ```mount -o rw,remount /system```
- create these two files:
    - ```/system/etc/init/remount-system.rc```
        ```
        on property:sys.boot_completed=1
            start remount-system
        service remount-system /system/bin/remount-system
            user root
        oneshot
        ```
    - ```/system/bin/remount-system```
        ```
        #!/system/bin/sh
        mount -o rw,remount /system
        ```
- run ```chmod +x /system/bin/remount-system```
now /system should be read-writeable.

If you need to use arm native bridge add ```/system/bin/enable_nativebridge``` to ```/system/bin/remount-system``` since from my observations it has to be re-enabled on each reboot.

## Arm NativeBridge
For details see [Arm-NativeBridge](https://github.com/SGNight/Arm-NativeBridge) and [libhoudini](https://github.com/Rprop/libhoudini) or [this file](arm-nativeBridge.md)

- Enable Native Bridge in settings
- Download [houdini.sfs](http://dl.android-x86.org/houdini/7_z/houdini.sfs) (7_z recommended)
- Copy it to ```/system/etc/```
- run the script ```/system/bin/enable_nativebridge```
