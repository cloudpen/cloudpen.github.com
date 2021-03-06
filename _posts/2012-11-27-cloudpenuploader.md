---
title: CloudPen Uploader参赛说明
layout: post
category: MyWork
---
CloudPen Uploader是一个基于金山快盘的作业提交系统。如果需要进行测试，则测试者必须具备一个快盘账号。请点击这里花一分钟进行申请，并下载快盘windows客户端进行安装、登录。快盘链接（http://www.kuaipan.cn）

感谢您能测试该软件。该软件的亮点是，无论学生在哪里提交作业，文件都将第一时间自动同步到教师安装了快盘客户端的电脑里。

以下将简单的向您介绍一下该软件的设计思路及使用方法。

一、软件设计说明

随着计算机网络技术在教育教学中的普及，信息化教学已经走入了常规课堂，越来越多学 科（尤其是计算机学科）的作业都需要以电子文档的形式提交。纵观现在的电子作业提交方式，不外乎以下几种：一是以U盘的形式进行拷贝，二是通过电子教室软 件即时提交，三是通过Email发送，四是通过IM软件进行发送，五是通过网络存储（如快盘、dropbox等软件）进行网络共享。下表将对这五种方式的 优缺点进行比较。

 
<table border=1>
<tr><td>提交方式</td><td>	优点</td><td>	缺点</td></tr>
<tr><td>U盘	</td><td>数据传输安全，能确保提交	</td><td>必须老师、学生都在，学生人数多时，提交耗费时间长。</td><td>
<tr><td>电子教室	</td><td>提交方便，无须逐人提交	</td><td>有时间、空间限制，且由于网络、软件等不确定因素，提交可能失败</td><td>
<tr><td>Email	</td><td>提交方便，无须逐人提交，无时间、空间限制，数据安全	</td><td>教师必须不断检测邮箱，并将附件下载，耗时较长</td><td>
<tr><td>IM软件</td><td>	提交方便，无须逐人提交，无时间、空间限制，数据安全	</td><td>教师需登录IM软件，且逐人保存</td><td>
<tr><td>网络存储共享</td><td>	提交方便，无须逐人提交，无时间、空间限制，数据安全，且提交后能主动同步到安装有存储客户端的电脑上	</td><td>不方便作业分班、归类</td><td></table>
表1

 

通过上述表格，我们可以发现，目前各种作业提交方式各有优劣，对学生而言，除使用U盘提交不够方便外，其他几种基于网络的方式都没有太大问题。而对于教师而言，这几种提交方式都 不大尽如人意，存在一定的缺陷。从教师的角度考虑，其理想状态是能在自己的电脑中，按照班级、作业次数等规则，设置几个文件夹，学生一旦通过网络提交作 业，就能够自动的按照规则保存到这几个文件夹中。这样，只要网络存在，无论是学生还是教师，作业的提交与收取都不再有时间和空间的限制，且不繁杂，不需要 消耗太多时间。

按照这样一个思路，笔者设计出一个基于快盘的作业提交系统，其需要达到如图1所示的目标：教师在电脑上安装快盘客户端，并在快盘目录下，按照作业提交规则，分班级、作业次数 新建相应的文件夹。而这些文件夹信息都会即时通过Web服务器上的“作业提交与查询界面”来呈现。此时学生就可以在该界面上选择班级文件夹、作业次数文件 夹，然后提交作业，一旦作业提交成功就会通过Web服务器自动上传到快盘相应目录中，而教师电脑中相应的目录下也会即时同步到学生的作业文件，以此来完成 作业的提交。

![](http://cloudpen-image.u.qiniudn.com/uploader.jpeg)

图1

二、软件使用方法

打开本站C.P. UPloader页面，也可点击这里的链接 <del>[程序链接]</del> （http://zhuyalin.cn/page/cloudpen-upload.html）。

页面中默认提供测试账号，如果您需要使用自己的账号进行尝试，请按页面提示信息，进入快盘授权页面，并使用您的账号进行登录。

登录完成后，在文件显示区显示出来的，将是您快盘目录下的一个测试文件夹，此时，该文件夹通过该程序向整个互联网开放，也就是说任何人登录该页面，都可以访问您公布出来的文件夹。

该程序提供给访问者四个功能。

一是建立文件夹：通过该功能，访问者可以在您的快盘目录下新建文件夹。此功能适用于学生在教师规定的作业提交文件夹下创建自己提交作业的文件夹。如：老师可以建立某个班级、第N次作业的文件夹，而学生则可以在此文件夹下建立个人提交作业的文件夹。

二是给文件夹加密：通过该功能，学生可以为自己的作业文件夹加密，以拒绝其他人访问。

三是在设置好的文件夹下通过点击“显示提交框”按钮来显示提交对话框，从而向相应的文件夹里提交文件，以完全作业的提交。

四是提供对文件的下载。

如此，学生通过以上四个功能建立并上传的文件及文件夹都可以及时同步到老师安装了客户端并登录的计算机上。（如果在测试时金山快盘的软件未及时同步，请您将快盘客户端退出后再登录即可）