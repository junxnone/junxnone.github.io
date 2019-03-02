> 从U盘或者硬盘启动

Name | Version
-- | --
HW | Raspberrypi 3B v1.2
OS | 20180627

--- 

# 1. 启动树莓派
# 2. 配置
配置树莓派为USB启动模式：
```
# echo program_usb_boot_mode=1 | sudo tee -a /boot/config.txt
``` 
## 2.1 检查
```
# vcgencmd otp_dump | grep 17:
```
输出应该为:
```
17:3020000a
```

# 3. 安装OS
烧写系统到USB Drive
## 3.1 检查
拔掉存储卡，插入USB Drive，启动树莓派
