
> This is "How to Fxxk the Greatwall for LAN with the Raspberrypi 3B?"
1. 需要墙外服务器
2. Raspberrypi 3B
---


# 1 Install shadowsocks
```
sudo pip install shadowsocks
```

```
pip install git+https://github.com/shadowsocks/shadowsocks.git@master
```
> x86&ubuntu下此命令会安装3.0.0, `pip install shadowsocsk` 会安装2.8.2, 被迫停止维护的版本

# 2 Install the polipo
```
sudo apt-get install polipo
```
## 2.1 Setup the polipo
```
sudo vi /etc/polipo/config
```
添加如下内容
```
logSyslog = true
logFile = /var/log/polipo/polipo.log
proxyAddress = "0.0.0.0"  

socksParentProxy = "127.0.0.1:1080"
socksProxyType = socks5
serverMaxSlots = 64  
serverSlots = 16  
serverSlots1 = 32  
```
## 2.2 Restart the polipo
```
sudo /etc/init.d/polipo restart
```

#  3 setup the shadowsocks Config file
```
vi shawdowsocks.json 
```
添加如下内容
```
{
  "server": "{your-server-ip}",
  "server_port": 40002,
  "local_port": 1080,
  "password": "{your-password}",
  "timeout": 600,
  "method": "aes-256-cfb"
}
```

# 4 Start the proxy
```
sudo sslocal -c shawdowsocks.json -d start
```
# 5 Setup the proxy for shell
```
sudo vi  ~/.bashrc
```
添加如下内容
```
export http_proxy=http://127.0.0.1:8123
```

# 6 Setup the proxy for apt
```
sudo vi /etc/apt/apt.conf.d/10proxy
```
添加如下内容
```
Acquire::http::Proxy "http://127.0.0.1:8123";
```
# 7 Setup the proxy for other windows/Linux/Phone in the LAN
Use this proxy to set your device:
```
http://xxx.xxx.xxx.xxx:8123
```
> xxx.xxx.xxx.xxx is your Raspberrypi 3B IP
