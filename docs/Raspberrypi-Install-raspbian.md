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
![image](https://user-images.githubusercontent.com/2216970/53687351-8ba42c80-3d6e-11e9-84fe-ab64ccad0844.png)
## etcher
![image](https://user-images.githubusercontent.com/2216970/53687353-92cb3a80-3d6e-11e9-96c5-3d19775dd12e.png)
