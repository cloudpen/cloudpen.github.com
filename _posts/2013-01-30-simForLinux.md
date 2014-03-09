---
title: ArchLinux宋体渲染
category: Linux
layout: post
---

先上效果图，宋体显示，数字和英文再也不发虚了，和XP里的效果相当。

<img src="http://cloudpen-image.u.qiniudn.com/simsunForLinux.png" width="640" height="480" />

你要是觉得还可以，下面说一下方法，非常非常简单。

一是安装微软字体。

	yaourt -S ttf-ms-fonts-zh_cn

当然，你也可以选择将宋体拷贝至/usr/share/fonts下进行安装。

二是新建一个宋体的配置文件。

	sudo vim /etc/fonts/conf.d/67-simsun-sharp.conf

并将以下内容拷贝到其中。

    <?xml version="1.0" encoding="UTF-8"?>
    
    <!DOCTYPE fontconfig SYSTEM "fonts.dtd">
    
    <!-- SimSun Configure File -->
    
    <fontconfig>
    
    <match target="font">
    
    <test qual="any" name="family">
    
    <string>SimSun</string>
    
    </test>
    
    <test name="weight" compare="less_eq" target="pattern">
    
    <const>medium</const>
    
    </test>
    
    <test compare="less_eq" name="pixelsize"><double>17</double></test>
    
    <test compare="more_eq" name="pixelsize"><double>12</double></test>
    
    <edit name="antialias" mode="assign"><bool>false</bool></edit>
    
    <edit name="embeddedbitmap" mode="assign"><bool>true</bool></edit>
    
    <edit name="hinting" mode="assign"><bool>true</bool></edit>
    
    <edit name="hintstyle" mode="assign"><const>hintfull</const></edit>
    
    <edit name="autohint" mode="assign" ><bool>false</bool>
    
    </edit>
    
    </match>
    
    </fontconfig>

然后注销系统再进入，打开这些特殊的网站，如163，sohu看看宋体的渲染效果吧。