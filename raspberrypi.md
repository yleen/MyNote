#Linux
# 安装系统
https://www.raspberrypi.org/software/operating-systems/#raspberry-pi-os-32-bit
傻瓜版导引
# 如何远程连接rpi
## 启动ssh
![[rpi_ssh.png]]
![[rpi_ssh2.png]]
## 获取rpi的ip
永恒的`ifconfig`  参考[[Linux#ifconfig详解]]
## 连接rpi
**首先 ssh连接**
`ssh pi@<ip address>`
### mac下远程连接桌面
**设置rpi开启vnc服务器**
[what is vnc?](https://www.realvnc.com/en/connect/)
**启动配置程序**
`sudo raspi-config`
![[rpi_config.png]]
选择Interface Options>设置VNC为Enable
**下载安装VNC**
 [点击下载](https://www.realvnc.com/en/connect/download/viewer/)
 **设置连接**
 点击左上角File>New connection, 将rip的Ip填入vnc service
 ![[rpi_vnc_config.png]]
 点击连接，输入密码即可。
 ### win下远程连接桌面
 **rpi安装xrdp**
 终端输入命令`sudo apt-get install xrdp`
 **rpi安装tightvncserver桌面服务**
 终端输入命令`sudo apt-get install vnc4server tightvncserver`
 **重启xrdp服务**
 `sudo /etc/init.d/xrdp restart`
 **win下启动mstsc，输入rpi的Ip**
 输入账号密码即可连接成功
 
# 两个问题
 
 1. 没有新建. node.red 文件
 2. 报错：
```bash
curl: (7) Failed to connect to raw.githubusercontent.com port 443: Connection refused
```
需要更改dns为8.8.8.8