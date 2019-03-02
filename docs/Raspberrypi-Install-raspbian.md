# Download the OS image
[latest image ](https://downloads.raspberrypi.org/raspbian_latest)
# Ubuntu
```
unzip xxxx-xx-xx-raspbian-stretch.zip
cd xxxx-xx-xx-raspbian-stretch
lsblk
sudo dd if=xxxx-xx-xx-raspbian-stretch.img of=/dev/sdX bs=4M conv=fsync status=progress
```
# Windows
- 1 [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/files/Archive/win32diskimager-1.0.0-install.exe/download)
- 2 [etcher](https://etcher.io/)
## Win32DiskImager
![win32diskimager write the raspbian image](https://github.com/junxnone/junxnone.github.io/blob/master/_img/win32diskimager.png)
## etcher
![etcher write the raspbian image](https://github.com/junxnone/junxnone.github.io/blob/master/_img/etcher.png)
