This is a guide on how to backup and restore any Termux distro without losing folders and files permissions
***
**Youtube Tutorial**

[![youtube tutorial](https://img.youtube.com/vi/3rHYsxcEr7k/0.jpg)](https://www.youtube.com/watch?v=3rHYsxcEr7k)
***
**Backup**<br/>
・Make sure your distro root folders (es. /dev, /proc) can be read by the owner<br/>
・If not, change the permissions of the folders to (400)<br/>
・Use the following command to backup your Termux "home" and "usr" folder
```
cd /data/data/com.termux/files
tar --format=gnu -pzcf /sdcard/termux-backup.tar.gz home usr
```
***
**Restore**<br/>
・Make sure to have storage permissions and the latest version of you Termux packages (supposing you have just installed Termux)
```
termux-setup-storage
pkg update && pkg upgrade
```
・Restore the "home" folder with the following commands:
```
cd /data/data/com.termux/files
rm -rf home
tar --same-owner -pzxf /sdcard/termux-backup.tar.gz home
```
・Then restore the "usr" folder as well
```
cd /data/data/com.termux/files
cp ./usr/bin/busybox ./tar
rm -rf usr
unset LD_PRELOAD
./tar -zxf /sdcard/termux-backup.tar.gz usr
exit
```
・You did it! You successfully restored your Termux distro!
***
・Termux official backup instructions (this guide doesn't mantain permissions):<br/>
https://wiki.termux.com/wiki/Backing_up_Termux
