[![youtube tutorial](https://img.youtube.com/vi/3rHYsxcEr7k/0.jpg)](https://www.youtube.com/watch?v=3rHYsxcEr7k)
***
**how to backup**

make sure your distro root folders (es. /dev, /proc) can be read by the owner, if not change the permissions of the files (400).

use the following command to backup your termux home and usr folder
```
cd /data/data/com.termux/files
tar --format=gnu -pzcf /sdcard/termux-backup.tar.gz home usr
```
***
**how to restore**

run termux and type the following commands

```
termux-setup-storage
pkg update && pkg upgrade
```

then restore the home folder
```
cd /data/data/com.termux/files
rm -rf home
tar --same-owner -pzxf /sdcard/termux-backup.tar.gz home
```
finally restore the usr folder
```
cd /data/data/com.termux/files
cp ./usr/bin/busybox ./tar
rm -rf usr
unset LD_PRELOAD
./tar -zxf /sdcard/termux-backup.tar.gz usr
exit
```

termux official backup instructions
https://wiki.termux.com/wiki/Backing_up_Termux
