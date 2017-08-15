---
title: 树莓派python3安装opencv
date: 2017-08-15 20:48:51
tags: linux arm python
---

用树莓派做图像tensorflow识别，安装opencv



```python
//安装cmake
wget https://cmake.org/files/v3.5/cmake-3.5.2.tar.gz
tar -xzvf cmake-3.5.2.tar.gz
cd cmake-3.5.2/
./bootstrap
make
sudo make install

//http://blog.csdn.net/qq_37910312/article/details/72866242
//opencv
cd /opencv
//https://codeload.github.com/opencv/opencv/zip/3.3.0
unzip 3.0.0.zip && cd opencv-3.0.0

 mkdir build && cd build
 
//自己找路径！
 cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local
PYTHON3_EXECUTABLE=/usr/bin/python3
PYTHON_INCLUDE_DIR=/usr/include/python3.4
PYTHON_LIBRARY=/usr/lib/arm-linux-gnueabihf/libpython3.4m.so
PYTHON3_NUMPY_INCLUDE_DIRS=/usr/lib/python3/dist-packages/numpy/core/include ..

make && sudo make install

import cv2
>>> print(cv2.__version__)

```



