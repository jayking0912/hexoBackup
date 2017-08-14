---
title: python3 mac安装opencv
date: 2017-08-08 20:48:51
tags: Mac opencv python
---

需要拍照提取照片进行训练，用到opencv, mac10.12，python3安装

0. brew tap homebrew/science  

1. brew install opencv3 --with-python3 --c++11 --with-contrib  --without-python
2. brew link --force opencv3  

安装成功与否测试一下

1. $ python3  
2. Python 3.5.1 (default, May 20 2016, 12:52:19)  
3. [GCC 4.2.1 Compatible Apple LLVM 7.3.0 (clang-703.0.31)] on darwin  
4. Type "help", "copyright", "credits" or "license" for more information.  
5. \>>> import cv2  

需要加入--without-python，否则报错，可能需要翻墙

参考：http://blog.csdn.net/willduan1/article/details/53898440