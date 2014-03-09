---
title: 解决修改Mysql密码后PHPMyAdmin无法登录问题
category: IT
layout: post
---

今天，把ubuntu上做的网站合并到win7下的XAMPP服务器上，由于两个环境下的mysql密码不相同，在win7下原来使用的空密码，所以在phpmyadmin下，将mysql的密码进行了更改。不过更改之后出现了以下错误：

迎使用 phpMyAdmin 2.9.0
    Probably reason of this is that you did not create configuration file. You might want to use setup script to create one.
错误
MySQL 返回：
> #1045 – Access denied for user: ‘root@localhost’ (Using password: NO)
在网上搜索一番，找到解决方法如下：

> 1、把/libraries目录下的config.default.php 覆盖phpmyadmin下的config.inc.php文件
> 2、然后修改phpmyadmin/config.inc.php文件
> $cfg['Servers'][$i]['user'] = ‘root’; // MySQL user
> $cfg['Servers'][$i]['password'] = ”; // MySQL password

如此即可。