---
title: let your Putty to display Chinese
category: IT
layout: post
---

I like to use putty to connecting the Linux. But, the chinese can't display normal in it.

It because the character encoding  is different between Linux & windows.

How to? 2 steps!

Step 1:

The same settings as the following figure putty.

<img src="http://cloudpen-image.u.qiniudn.com/putty1.PNG" width=480 height=320 />

![](http://cloudpen-image.u.qiniudn.com/putty2.PNG)

Step 2:

After logging in linux, enter the following in Terminal:

	export LC_ALL='zh_CN.utf8'

Ok,that's all!