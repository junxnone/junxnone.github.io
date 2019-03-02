Name|Version
---|---
HW|Raspberrypi 3B v1.2
OS| 20180627
--- 
# 1. 启动树莓派
# 2. 开启USB启动模式：
```
# echo program_usb_boot_mode=1 | sudo tee -a /boot/config.txt
``` 
# 3. 重启树莓派，并检查设置
```
# vcgencmd otp_dump | grep 17:
```
输出应该为:
```
17:3020000a
```

# 4. 烧写系统到USB Drive
# 5. 拔掉存储卡，插入USB Drive，启动树莓派
