---
title: Linux下去除Windows密码
category: Linux
layout: post
---

今天遇到一件囧事，长时间不进Windows环境结果把自己设置的密码给忘记了，于是便发了一条微博。热心朋友一大堆，给我推荐各种各样的方法，自己也到网上搜了一搜，原来在Linux下去除Windows的密码是那么简单。方法步骤如下：

一、安装工具chntpw

这个工具应该在各大发行版的官源里都存在（Linux对Windows的安全环境考虑真是没得说。==！）。直接用你的发行版里最常用的安装方式安装即可。

比如Archlinux– sudo pacman -S chntpw

二、使用工具

挂载windows系统分区盘，进入到 windows/system32/config中，就地打开终端，运行如下命令：

sudo chntpw SAM

会得到如下提示：


> User Edit Menu:
> 
> 1 – Clear (blank) user password
> 
> 2 – Edit (set new) user password (careful with this on XP or Vista)
> 
> 3 – Promote user (make user an administrator)
> 
> (4 – Unlock and enable user account) [seems unlocked already]
> 
> q – Quit editing user, back to user select
> 
> Select: [q] >

很显然，选1清除密码;选2重设密码;选3不知不觉提升用户权限，哈哈;选4启用或者关闭某个用户。我果然选1，重启进入Windows一路无阻！