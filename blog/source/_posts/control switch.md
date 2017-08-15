---
title: 树莓派加入按钮控制饮水机开关
date: 2017-07-20 20:48:51
tags: linux arm python
---

用树莓派控制饮水机和打印机开关，公司正常8.00到17.00,周一到周五上班，因此将拖线板火线接在继电器上，用树莓派GPIO口控制继电器，crontab设置定时任务就可以了,对于特殊情况，需要加入个按钮来控制开关

### 一。继电器开关



```python
//switchon.py

import RPi.GPIO as GPIO

import time

# BOARD  ^  ^   ^    ^   ^  ^    ^ BCM

GPIO.setmode(GPIO.BCM)

#    ^   ^  1 --GPIO1

GPIO.setup(18,GPIO.OUT)

GPIO.output(18,GPIO.LOW)



//swichoff.py

import RPi.GPIO as GPIO

import time

# BOARD  ^  ^   ^    ^   ^  ^    ^ BCM

GPIO.setmode(GPIO.BCM)

#    ^   ^  1 --GPIO1

GPIO.setup(18,GPIO.OUT)

GPIO.output(18,GPIO.HIGH)



//buttuon
import RPi.GPIO
import time
import os

RPi.GPIO.setmode(RPi.GPIO.BCM)

RPi.GPIO.setup(18,RPi.GPIO.OUT)
RPi.GPIO.setup(16, RPi.GPIO.IN, RPi.GPIO.PUD_UP)

try:
        while(1):
                time.sleep(0.01)

                if(RPi.GPIO.input(16) == 0):
                                print('get')
                                RPi.GPIO.output(18,not RPi.GPIO.input(18))
                                time.sleep(2)
                else:
                                time.sleep(0.2)
except KeyboardInterrupt:
        pass
#RPi.GPIO.cleanup()

```



### 二。crontab

输入crontab -e 进入编辑定时器

7点55启动

`55 07 * * 1,2,3,4,5 python3 /home/pi/switchon.py`

16点45关闭

`45 16 * * * python3 /home/pi/switchoff.py`

每天启动一次按钮程序，防止挂掉（带锁存在不启动）

`39 13 * * * flock -xn /home/pi/my.lock -c 'python3 /home/pi/button.py'`

