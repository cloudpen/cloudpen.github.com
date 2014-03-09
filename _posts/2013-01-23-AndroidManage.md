---
title: Linux下android管理工具
category: Linux
layout: post
---


Windows下面的android管理工具层出不穷、各式各样，Linux下就显得捉襟见肘、少得可怜了。不过我们知道Linux下调试Android有一个伟大的工具叫Adb，所以有一款基于Adb的手机管理工具叫做Qtadb，下面就来简单的介绍一下这个工具的使用方法。

第一步，连接手机

将手机的调试模式打开（注意，手机必须root，且安装了busybox），然后用Usb的方式将它与计算机连接起来，（如果是archlinux，强烈建议安装 android-udev）， 使用lsusb查看你的usb连接文件，你可能会得到以下数据。

	[cloudpen@cloudpen local]$ lsusb
	Bus 002 Device 010: ID 04e8:68c6 Samsung Electronics Co., Ltd
	Bus 002 Device 004: ID 5986:0242 Acer, Inc
	Bus 006 Device 002: ID 1d57:0008 Xenta
	Bus 008 Device 002: ID 0a5c:2150 Broadcom Corp. BCM2046 Bluetooth Device
	Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
	Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
	Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
	Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
	Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
	Bus 006 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
	Bus 007 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
	Bus 008 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub

我们可以看到，第一项内容就是我的手机。

第二步，配置手机

创建相关配置文件：sudo vim /etc/udev/rules.d/51-android.rules

在其中输入：


	SUBSYSTEM==”usb”, ATTR{idVendor}==”04e8″, MODE=”0666″
	SUBSYSTEM==”usb”,ATTR{idVendor}==”04e8″,ATTR{idProduct}==”68c6″,SYMLINK+=”android_adb”
	SUBSYSTEM==”usb”,ATTR{idVendor}==”04e8″,ATTR{idProduct}==”68c6″,SYMLINK+=”android_fastboot”


其中的idVendor和idProduct就是lsusb中查到的对应的值。

再次执行udevadm control –reload-rules，保证运行规则加载成功（最好给刚才的规则文件加上运行的权限）。

同时，编辑 ～/.android/adb_usb.ini 文件，加入0x04e8，即0x加上你的idVendor。

第三步，下载Qtadb

Archlinux用户可以直接yaourt，其他用户可能需要翻墙下载这个文件了，地址在http://qtadb.wordpress.com/，Cloudpen也提供一个下载链接。http://s.yunio.com/Mbcgeu

Qtadb是一个可执行的文件，执行后，会要求你选择adb的工作位置，如果你的机器里已经有adb了，直接定位，如果没有，Cloudpen的下载包里也有，直接定位即可。

第四步，应用Qtadb

这一步就不用说了吧，打开软件后就可以直接使用了。
