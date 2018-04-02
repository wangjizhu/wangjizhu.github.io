---
layout: post
title:  "ubuntu和win7系统时间不一致"
date:   2018-02-07 
categories: linux
---

ubuntu+win7 每次切换时间都不一样 怎么都不行 用一下这个方法


# ubuntu下面操作


先在ubuntu下更新一下时间，确保时间无误：

``sudo apt-get install ntpdate

``sudo ntpdate time.windows.com


然后将时间更新到硬件上：

``sudo hwclock --localtime --systohc




 
