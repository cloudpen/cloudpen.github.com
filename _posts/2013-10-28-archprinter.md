---
title: Archlinux网络打印服务的便捷安装
layout: post
category: Linux
---

每次做完Linux系统，连打印机总是要好长时间。今天下午又做了一遍，并将过程整理了一下，全程也就不到20分钟的样子。具体到步骤，为以下几项命令。

1. 参照wiki安装基本程序

> sudo pacman -S cups ghostscript gsfonts samba

并启动服务

> sudo systemctl enable cups

2. 不要参照WIKI，安装打印驱动

> yaourt -S foo2zjs  //64位系统下，使用HP打印机，强烈建议安装此驱动。

3. 不要使用Gnome3.10自带的打印机管理

> sudo pacman -S system-config-printer

然后运行 system-config-printer，安装打印机。DO IT！