---
layout: post
title:  ESP32-C3刷写MicroPython
categories: [ESP32,MicroPython]
tags:    [IoT,ESP32]
date:   2022-03-29 09:00:00

---

之前某宝合宙家的开发板子非常便宜，9.9包邮即可买到ESP32-C3的板子。于是就下单屯了几张：

![NB]({{site.BASE_PATH}}/img/esp32/esp32_install_micropython_01.png)

ESP32开发板是物联网开发中比较常见的板子，既便宜性价比又高，支持WiFi和蓝牙模块。

**ESP32**一般常用的开发方式如下几种：

* Arduino (C++或C语音)

* MicroPython（Python）

* ...

因为Python相对C系列语言入门更简单写，所以就想用**ESP32** 刷个**MicroPython**如个门。

ESP32刷MicroPython有好多方法，比如**Thonny**的Tools就支持安装、乐鑫的Flash 下载工具等等，以下将介绍使用esptool的命令行安装：

### 0. 安装**esptool**工具

> pip install esptool 

安装可使用如下命令查看当前esptool的版本，并验证是否安装成功

> esptool.py version

如：esptool.py v3.3类似信息则证明安装成功。



[官方镜像地址

拉倒页面最底部，下载要刷写的**bin**文件

![]({{site.BASE_PATH}}/img/esp32/esp32_install_micropython_02.png)

> **注意**：Release最新v1.18版本对 **neopixel**库使用会报错，若用到它建议刷Nightly builds的最新版本

### 2. 将ESP32连接电脑，查看基本信息

输入如下指令，查看当前设备的端口

> esptool.py chip_id

得到如下输出，记住**Serial port**，下一步刷MicroPython用：

> esptool.py v3.3  
> Found 1 serial ports  
> **Serial port COM4**  
> Connecting....  
> Detecting chip type... ESP32-C3  
> Chip is ESP32-C3 (revision 3)  
> Features: Wi-Fi  
> Crystal is 40MHz  
> MAC: 60:55:f9:71:b5:6c  
> Uploading stub...  
> Running stub...  
> Stub running...  
> Warning: ESP32-C3 has no Chip ID. Reading MAC instead.  
> MAC: 60:55:f9:71:b5:6c  
> Hard resetting via RTS pin...

### 3. 擦写Flash（erase_flash）

官方建议首次刷MicroPython执行这一步：

> If you are putting MicroPython on your board for the first time then you should first erase the entire flash using:

执行命令：

> esptool.py --chip esp32-c3 --port **COM4** erase_flash

如上命令中**COM4**为步骤2中的Serial port，执行结果如下：

> esptool.py v3.3  
> Serial port COM4  
> Connecting....  
> Chip is ESP32-C3 (revision 3)  
> Features: Wi-Fi  
> Crystal is 40MHz  
> MAC: 60:55:f9:71:b5:6c  
> Uploading stub...  
> Running stub...  
> Stub running...  
> Erasing flash (this may take a while)...  
> Chip erase completed successfully in 12.7s  
> Hard resetting via RTS pin...

### 4. 刷写MicroPython

执行如下命令：

> esptool.py --chip esp32-c3 --port **COM4** --baud 460800 write_flash -z **0x0** path:\esp32c3-20220117-v1.18.bin

**--port COM4**:是步骤2中获得的

**-z 0x0** :这个不能错，错了刷完会一直报些莫名其妙的错误

**path:\esp32c3-20220117-v1.18.bin**：是步骤2中下载的bin的路径和文件名

运行结果如下：

> esptool.py v3.3  
> Serial port COM4  
> Connecting....  
> Chip is ESP32-C3 (revision 3)  
> Features: Wi-Fi  
> Crystal is 40MHz  
> MAC: 60:55:f9:71:b5:6c  
> Uploading stub...  
> Running stub...  
> Stub running...  
> Changing baud rate to 460800  
> Changed.  
> Configuring flash size...  
> Flash will be erased from 0x00001000 to 0x00163fff...  
> Compressed 1450160 bytes to 865812...  
> Wrote 1450160 bytes (865812 compressed) at 0x00001000 in 25.8 seconds (effective 448.9 kbit/s)...  
> Hash of data verified.
> 
> Leaving...  
> Hard resetting via RTS pin...

看到如上信息即表示**MicroPython**刷入成功

### 5. Hello ESP32

使用**Thonny IDE**的Shell窗口写一个Hello World.

[下载安装](https://thonny.org/) Thonny过程略...

* 使用Thonny连接ESP32

如下图**Tools**->**Options...**->选择第二个**Interpreter**项->**device**下拉选择**MicroPython（ESP32）**-> **Port**下拉选择当前ESP32设备的端口

![]({{site.BASE_PATH}}/img/esp32/esp32_install_micropython_03.png)

如上图，点击**OK按钮**，显示出设备的基本信息，并出现**>>>**，则证明连接成功
* 尝试打印Hello World   

在命令行输入下边指令并回车：

> print("Hello ESP32")

![]({{site.BASE_PATH}}/img/esp32/esp32_install_micropython_04.png)

看到如上图所示信息，即刷写完成。



### -- The End --
