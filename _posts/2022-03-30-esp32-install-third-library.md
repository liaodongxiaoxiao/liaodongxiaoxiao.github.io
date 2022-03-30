---
layout: post
title:  ESP32下MicroPython 引入三方库
categories: [ESP32,MicroPython]
tags:    [IoT,ESP32]
date:   2022-03-29 12:00:00

---

      在ESP32板子上使用MicroPython开发时，经常会用到三方库。与在Python中的**pip**类似，MicroPython也提供了**upip**工具来安装三方库。

以下将介绍**upip**的使用方法（以下均在控制台操作）：

### 0. ESP32 通过WiFi联网

```python
>>> import network # 引入网络库
>>> sta_if = network.WLAN(network.STA_IF) # 获取wlan对象
>>> sta_if.active(True) # 激活
>>> sta_if.connect('<your ESSID>', '<your password>') # 连接WiFi，WiFi名字和WiFi密码
>>> sta_if.isconnected() # 检查WiFi是否连接成功
>>> sta_if.ifconfig() # 查看ESP32的IP地址
```

结果如下：

![NB]({{%20site.BASE_PATH}}/img/esp32/esp32_upip_01.png)

### 1. 使用upip安装三方库

```python
>>> import upip # 引入upip工具包
>>> upip.install("三方库名") # 安装三方库
```

以安装 **umqtt** 库为例，操作结果如下：

![NB]({{ site.BASE_PATH}}/img/esp32/esp32_upip_02.png)

### 2. 验证三方库是否安装成功

* 查看文件目录是否存在
  
  ```python
  >>> import os
  >>> os.listdir("lib")
  ```
  实际操作结果如截图：
  ![NB]({{ site.BASE_PATH}}/img/esp32/esp32_upip_03.png)

* 通过代码引入验证
  
  ```python
  >>> import 三方库
  >>> 具体使用
  ```
  实际操作结果截图：
  ![NB]({{ site.BASE_PATH}}/img/esp32/esp32_upip_04.png)
  
  
-- The End --
