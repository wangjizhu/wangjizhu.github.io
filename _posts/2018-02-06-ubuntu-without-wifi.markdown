---
layout: post
title:  "thinkpad在ubuntu下面没有无线网卡的解决"
date:   2018-02-06 
categories: linux
---

太多坑 跳了很多 写点日志 免得又跳 跳了很多

自己看 只写要点


# Linux 安装
T460p 挂了 第二次挂了。。。 屏幕排线挂了 修好了发现尼玛grub不见了  
本来装的双系统 怎么直接进windows了。。。。  
重新装吧 非常简单
1. 下载一个ubuntu的镜像 现在是16.。。。
2. 用一个叫什么的工具把镜像写入u盘
3. u盘启动进入live cd
4. 桌面上有一个图标直接装即可
5. 记得装纯英文的 你会后悔的
* 坑 也没有什么坑 就是装个系统这么麻烦Linux分区 要注意跟win不兼容 其他都是常识 ext4  要有一个swap
在先win后lin的情况下他会自动给你注入grub2 仔细观察安装进度下面会显示 installing grub2
然后非常自觉地把ubuntu写到了第一个。。。。

# 无线网卡驱动
在live CD载入的系统中 无线一点问题都没有 正常上网
但是安装完成进去后发现。。。。。。 没有无线网卡了 也就是说必须插入网线 这是一个什么鬼  
幸好有个乐视手机 usb插上去 勾选“usb共享上网”  
然后手机被识别成一个usb网卡就自动链接了。。。
然后就是 搜了一整天解决方案 什么都试过了 最后才成功 所以记录下：  
1. 首先使用uname -a查看这个版本的linux内核4.13.0-32-generic
2. 然后用ifconfig -a 看没有wlan0 没有无线网卡驱动
3. lshw 列举硬件列表查看 实际上无线网卡是有的 但是状态不对 product一项显示器设备是啥product: Wireless 8260 这是一个intel的无线网卡
4. 在iwlwifi网站上查看 实际上4.1内核集成了对这款网卡的驱动的 但是你妹就是不识别  
[https://wireless.wiki.kernel.org/en/users/Drivers/iwlwifi](https://wireless.wiki.kernel.org/en/users/Drivers/iwlwifi)  
这个网站往下面翻 翻到自己的网卡 和内核号对应的驱动下载 下来是一个压缩包 解开里面有.ucode文件
按照说明文件cp到这里  
``# cp iwlwifi-*.ucode /lib/firmware``  

最后重启就好
可以先update一下内核号  
``sudo apt-get install Linux-generic-lts-wily``  
重启了无数次没用 最后拔了电源电池也没有 后来自己就有了 不知所云
后来稳定的一比



 
