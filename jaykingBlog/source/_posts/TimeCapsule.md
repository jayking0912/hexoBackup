---
title: 使用树莓派制作time Capsule
date: 2017-09-15 20:48:51
Tags: timemachine raspberry linux
---
​	一直在寻找最省成本的备份方案，目前用树莓派作为备份服务器，省电，便宜，但测试效果不是很好，备份速度慢，对备份速度没要求的可以用。

材料：

树莓派3B

2T硬盘

硬盘转接线



## 硬盘格式化

现在MACOS 上把硬盘格式化，hfs,一个分区，如果备份比较大可以先连mac进行本地备份，备份完成需要需要关掉journal功能，因为linux只支持读写non-journaled HFS+

```
#列出list
diskutil list
#关闭Journal(0s2改成自己的)
$ diskutil disableJournal disk0s2
Journaling has been disabled on disk0s2
```



## 挂载硬盘

##### 1 安装HFS+工具

`sudo apt-get install hfsplus hfsutils hfsprogs`

##### 2 插上硬盘到树莓派

挂载

```bash 
sudo fdisk -l 

sudo mkdir /tm
#改成自己的sdxx
sudo mount /dev/sda2 /tm

sudo chmod 777 tm
```

##### 3 安装配置netatalk

Netatalk 是一个免费开源的 AppleTalk 通信协议的实现，[Linux](http://lib.csdn.net/base/linux) 或者 BSD 系统通过它可以充当 Mac 的文件服务器 (AppleShare File Server, 网络协议是 AFP)、AppleTalk 路由、打印服务器等。）

sudo apt-get install netatalk

sudo vim  /etc/netatalk/AppleVolumes.default （[AppleVolumes.default 文档](http://netatalk.sourceforge.net/2.0/htmldocs/AppleVolumes.default.5.html)）
在最后一行添加：/mnt/TimeCapsule "Time Capsule" options:tm  保存退出

##### 4 安装配置配置Avahi

Avahi 是 Apple’s Zeroconf 协议的开源实现，实现类似 Bonjour 的功能，它可以让你在 Mac 系统里自动发现你的 Linux 计算机。

sudo apt-get install avahi-daemon libnss-mdns
sudo vim /etc/nsswitch.conf
在hosts:后添加“mdns”，添加后为：hosts:      files mdns4_minimal [NOTFOUND=return] dns mdns4 mdns
sudo vim /etc/avahi/services/afpd.service
添加如下内容：
<?xml version="1.0" standalone='no'?><!--*-nxml-*-->
<!DOCTYPE service-group SYSTEM "avahi-service.dtd">
<service-group>
​    <name replace-wildcards="yes">%h</name>
​    <service>
​        <type>_afpovertcp._tcp</type>
​        <port>548</port>
​    </service>
​    <service>
​        <type>_device-info._tcp</type>
​       <port>0</port>
​        <txt-record>model=Xserve</txt-record>
​    </service>
</service-group>

（3）重启服务

sudo service netatalk restart
sudo service avahi-daemon restart