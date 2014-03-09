---
title: Archlinux Wiki,So great!
layout: post
category: Linux
---

Wiki真的非常棒，汇集众人的智慧，几乎所有的问题都能在一个权威的Wiki上解决。Archlinux的Wiki更是如此。从安装到后期的维护，它都是使用者最大的后援团。但，一般的Wiki都是实时、在线的，有的时候脱机了，想查阅一个问题，还真是有那么一些不顺。Archlinux想用户所想，建立了一个离线的Wiki，而且使用起来非常方便。具体如下：

1. 安装

主要是安装两个包包，一是arch-wiki-docs，另一个是arch-wiki-lite。都是Pacman吃下来的，可以与在线的Wiki实时同步、更新，真的很棒。

2. 设置与使用

主要是设置语言及打开方式，可以通过wiki-search –lang来查看支持语言，用export wiki_lang=” 语言” 来指定语言。

通过export wiki_browser=’/usr/bin/google-chrome’来指定打开文件的浏览器。

而使用的方法则通过

wiki-search 关键字 来查看有哪些Wiki文档，相应的文档后面都有编号，然后 可以通过

wiki-search-html 编号  在浏览器中打开相应的文档。真的非常棒！

3. 实现原理

其实，是将Wiki的文档网页缓存到了本地，然后使用wiki-search来查找而已。用grep也可以进行查找定位。