---
title: Linux下mtp连接方法
layout: post
category: Linux
---

Android 4.1，大容量存储的功能好像被精简掉了，在我的ME172V上怎么找也找不到。Windows下还好，我还可以通过各种手机助手软件的文件管理功能向Me172V上传输文件，但在Linux下就变得困难了。

Android 4.1下在存储的选项中有两个可选项，一是MTP，二是相机。在使用这两个选项分别连接Linux时,相机功能中可以看到机器中的图片，但不能对其他文件做操作，而MTP是没有任何反应的，因此，我们要做的就是加载Linux对于MTP协议的支持，并让文件管理器可以通过该协议来操作设备中的文件。方法如下：

一、安装支持文件

> sudo apt-get install mtpfs libfuse-dev libmad0-dev

二、建立文件挂载点，并设备挂载点的权限

> sudo mkdir /media/mtp

> sudo chmod 775 /media/mtp

三、打开设备上的MTP选项，挂载MTP设备

> sudo mtpfs /media/mtp

四、在文件管理器操作设备文件

<img src="http://cloudpen-image.u.qiniudn.com/mtpmanage.jpg" width="640" height="480" />

五、用完后，卸载设备

> sudo umount /media/mtp