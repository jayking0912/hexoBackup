---
title: 在树莓派重新安装python3
Tags: python3 raspberry linux
---
最近写的程序 运行老是报 ssl 错误，没办法只好重装python3

## 第一步先升级

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

然后进入下载的目录下载

## 安装python 3.4需要的依赖。

##### 有些东西可能已经存在了，会自动忽略。

```
sudo apt-get install build-essential libsqlite3-dev sqlite3 bzip2 libbz2-dev libssl-dev openssl libgdbm-dev liblzma-dev libreadline-dev libncursesw5-dev
```

```
wget https://www.python.org/ftp/python/3.4.3/Python-3.4.3.tgz
tar zxvf Python-3.4.3.tgz
```

```
cd ./Python-3.4.3
./configure --prefix=/opt/python3.4
make
make
sudo make install
```

在make命令后再执行一次make命令，既可看仍有哪些Python模块无法编译，然后排查原因（通常是没安装相应的依赖包）。



## 创建软链接。

创建之后，打python3就能启动python 3.4.3了。

第一行删除已有的指向python 3.2.3的软链接。

第二行创建/usr/bin/python3这个软链接指向python 3.4.3。

第三行创建一个pip的软链接。pip已经被官方集成到python3.4里，用它安装pypi上的第三方模块很方便。

```
sudo rm /usr/bin/python3
sudo ln -s /opt/python3.4/bin/python3.4   /usr/bin/python3
sudo rm /usr/bin/pip3
sudo ln -s /opt/python3.4/bin/pip3.4         /usr/bin/pip3
```

