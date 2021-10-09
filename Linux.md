---
title: Linux命令记录 #文章页面上的显示名称，可以任意修改，不会出现在URL中
date: 2021-3-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: #文章分类目录，可以为空，注意:后面有个空格
tags: [Linux] #文章标签，可空，多标签请用格式[tag1,tag2,tag3]，注意:后面有个空格
description: Linux#概要信息
---
# 常用命令

## 删除文件夹
`rm -rf` -r 向下递归，不管有多少级目录，一并**删除**。 -f 直接强行**删除**，没有任何提示

## 复制文件到另一位置
`cp <source> <destination>`

## 更改文件名
`mv <old name> <new name>`

## 显示隐藏文件
`ls -a` 可显示.开头的文件

## 输出文件内容到Terminal
**cat**
`cat <file name>`
`cat -n <file name>` 输出内容并显示行号
**more**
`more` 与 `cat` 相似，都可以查看文件内容，所不同的是，当一个文档太长时， `cat` 只能展示最后布满屏幕的内容，前面的内容是不可见的。这时候可用 `more` 逐行显示内容。
`more <filename>`
`more +100 <filename>` 从第100行开始显示
**less**
`less` 与 `more` 相似，不过 `less` 支持上下滚动查看内容，而 `more` 只支持逐行显示。
`less <filename>`
`less +100 <filename>` 从第100行显示

## 查找文件，手册路径
`whereis bash` 显示文件和路径
`whereis -b bash` 仅查找binary
`whereis -m bash`仅查找manual

# 程序后台运行

## 不退出终端
`<command> &`
在执行的命令后加`&`即可将运行的程序运行在后台。
**查看后台运行的程序**
`jobs`或`jobs -l` 带-l会显示进程id

**将后台程序转到前台**
`fg` 当后台只有一个程序时
`fg %<job id>` 后台多个程序时
**清理后台程序**
`kill -9`

## 退出终端继续运行
`nohup <command> &`
关闭终端进程不会终止

参考： https://linuxize.com/post/how-to-run-linux-commands-in-background/

# Ctrl C 与Ctrl Z的区别
https://superuser.com/questions/262942/whats-different-between-ctrlz-and-ctrlc-in-unix-command-line

# Linux 不明原因卡死
有可能是按到了`ctrl + s`，在linux中ctrl+s是锁定屏幕的快捷键，若解锁，需按下`Ctrl + q`

# 页面滚动
`ctrl + shift + Up` + `ctrl + shift + down`

# ifconfig详解
许多windows非常熟悉ipconfig命令行工具，它被用来获取网络接口配置信息并对此进行修改。Linux系统拥有一个类似的工具，也就是ifconfig(interfaces config)。通常需要以root身份登录或使用sudo以便在Linux机器上使用ifconfig工具。依赖于ifconfig命令中使用一些选项属性，ifconfig工具不仅可以被用来简单地获取网络接口配置信息，还可以修改这些配置。

1．命令格式：

`ifconfig [网络设备] [参数]`

2．命令功能：

ifconfig 命令用来查看和配置网络设备。当网络环境发生改变时可通过此命令对网络进行相应的配置。

3．命令参数：

`up` 启动指定网络设备/网卡。

`down` 关闭指定网络设备/网卡。该参数可以有效地阻止通过指定接口的IP信息流，如果想永久地关闭一个接口，我们还需要从核心路由表中将该接口的路由信息全部删除。

`arp` 设置指定网卡是否支持ARP协议。

`-promisc` 设置是否支持网卡的promiscuous模式，如果选择此参数，网卡将接收网络中发给它所有的数据包

`-allmulti` 设置是否支持多播模式，如果选择此参数，网卡将接收网络中所有的多播数据包

`-a` 显示全部接口信息

`-s` 显示摘要信息（类似于 netstat -i）

`add `给指定网卡配置IPv6地址

`del` 删除指定网卡的IPv6地址

`<硬件地址> `配置网卡最大的传输单元

`mtu<字节数>` 设置网卡的最大传输单元 (bytes)

`netmask<子网掩码>` 设置网卡的子网掩码。掩码可以是有前缀0x的32位十六进制数，也可以是用点分开的4个十进制数。如果不打算将网络分成子网，可以不管这一选项；如果要使用子网，那么请记住，网络中每一个系统必须有相同子网掩码。

`tunel` 建立隧道

`dstaddr` 设定一个远端地址，建立点对点通信

`-broadcast<地址>` 为指定网卡设置广播协议

`-pointtopoint<地址>` 为网卡设置点对点通讯协议

`multicast` 为网卡设置组播标志

`address` 为网卡设置IPv4地址

`txqueuelen<长度>` 为网卡设置传输列队的长度

4．使用实例：

实例1：显示网络设备信息（激活状态的）

命令：

`ifconfig`

输出：
```shell
[root@localhost ~]# ifconfig  
eth0      Link encap:Ethernet  HWaddr 00:50:56:BF:26:20    
          inet addr:192.168.120.204  Bcast:192.168.120.255  Mask:255.255.255.0  
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1  
          RX packets:8700857 errors:0 dropped:0 overruns:0 frame:0  
          TX packets:31533 errors:0 dropped:0 overruns:0 carrier:0  
          collisions:0 txqueuelen:1000   
          RX bytes:596390239 (568.7 MiB)  TX bytes:2886956 (2.7 MiB)  
  
lo        Link encap:Local Loopback    
          inet addr:127.0.0.1  Mask:255.0.0.0  
          UP LOOPBACK RUNNING  MTU:16436  Metric:1  
          RX packets:68 errors:0 dropped:0 overruns:0 frame:0  
          TX packets:68 errors:0 dropped:0 overruns:0 carrier:0  
          collisions:0 txqueuelen:0   
          RX bytes:2856 (2.7 KiB)  TX bytes:2856 (2.7 KiB)
```

**说明：**

-   **eth0** is the first [Ethernet](https://www.computerhope.com/jargon/e/ethernet.htm) interface. (Additional Ethernet interfaces would be named **eth1**, **eth2**, etc.) This type of interface is usually a [NIC](https://www.computerhope.com/jargon/n/nic.htm) connected to the network by a [category 5](https://www.computerhope.com/jargon/c/cat5.htm) cable.
-   **lo** is the [loopback](https://www.computerhope.com/jargon/l/loopback.htm) interface. This is a special network interface that the system uses to communicate with itself.
-   **wlan0** is the name of the first [wireless network](https://www.computerhope.com/jargon/w/wifi.htm) interface on the system. Additional wireless interfaces would be named **wlan1**, **wlan2**, etc.

第一行：连接类型：`Ethernet`（以太网）`HWaddr`（硬件mac地址）

第二行：网卡的IP地址、子网、掩码

第三行：`UP`（代表网卡开启状态）`RUNNING`（代表网卡的网线被接上）`MULTICAST`（支持组播）`MTU:1500`（最大传输单元）：1500字节

第四、五行：接收、发送数据包情况统计

第七行：接收、发送数据字节数统计信息。

趣闻：[mac 中ifconfig eth为什么代表的不一样](https://stackoverflow.com/questions/23098273/why-is-wi-fi-called-en0-like-ethernet-on-a-mac-os-x)