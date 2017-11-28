---
title: python3 转成 linux 可执行文件
date: 2017-03-12 20:48:51
tags: linux arm python
---

最近买了个arm工控机，居然不能运行 make命令，自然装不了python,只能想办法变成linux执行文件，正好手头有树莓派，运行环境相同（arm linux）

1.安装pyinstaller

sudo pip3 install pyinstaller



2.cd 到需要编译成文件夹



3. sudo /opt/python3.4/bin/pyinstaller -F xxx.py

找到安装pyinstaller的目录，我的是/opt/python3.4/bin/pyinstaller

 -F 打包成一个程序， 然后会看到新增加了两个目录build和dist，dist下面的文件就是可以发布的可执行文件

