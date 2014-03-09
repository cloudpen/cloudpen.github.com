---
title: Archlinux与Win8双系统菜单的修复
layout: post
category: Linux
---

Windows8与Linux在同一台电脑上存在目前还是个问题，因为Windows8采用了新的引导机制，这使得Linux系统在使用Grub菜单进行引导时无法获取它的信息。但我们还是可以通过手工修改来实现多系统引导的。

以下内容建立在该假设环境下：

  假设电脑中已经安装了Linux系统，在此基础上又安装了Win8，并且完成了Win8后只能启动win8系统。
步骤如下：

1.准备ArchLinux的系统盘，从该系统盘启动。

2.进入ArchLinux安装环境后，确保系统已经联网，运行以下命令：

  	mount /dev/sdax  /mnt  --挂载 / 分区至mnt下
 	mount /dev/sday  /mnt/home  --挂载 /home 分区到 mnt/home下
  	arch-chroot /mnt  --进入系统配置状态
  	pacman -S grub-bios  --安装grub-bios准备进行修复
  	grub-install --target=i386-pc --recheck /dev/sda  --安装grub到sda
  	cp /usr/share/locale/en@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

  	grub-mkconfig -o /boot/grub/grub.cfg  --生成新的grub.cfg文件
  	
	sudo blkid --查看你的windows所在盘的uuid，并且记录下来
  	
	nano /boot/grub/grub.cfg --编辑grub.cfg，并在其中加入以下内容（将以下64DAA6CADAA69836全部替换成上一步查到的uuid）

   	menuentry 'Microsoft Windows 8 (on /dev/sda1)' --class windows --class os $menuentry_id_option 'osprober-chain-6A54E1A754E175EB' {
   	insmod part_msdos
   	insmod ntfs
   	set root='hd0,msdos1'
   	if [ x$feature_platform_search_hint = xy ]; then
    	  search --no-floppy --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1  64DAA6CADAA69836
   	else
    	  search --no-floppy --fs-uuid --set=root 64DAA6CADAA69836
   	fi
    	  drivemap -s (hd0) ${root}
    	  chainloader +1
   	 }

3.上述步骤操作完成后，退出chroot，并且使用umount缷载分区，然后重启计算机，你会看到grub菜单已经出现，并且加入win8的选项。