---
title: Ubuntu 12.04下修改默认启动方式及模式切换
date: '2013-08-08'
description: ubuntu12.04启动方式
categories: resolution
tags: [Ubuntu,关闭Xserver,命令行模式 ]
---

##修改默认启动方式##

进入ubuntu的命令行模式，比如在安装Nvidia驱动的时候，就必须要关闭Xserver.方式：

启动终端，输入

    $echo “false” | sudo tee /etc/X11/default-display-manager

重新启动就可以直接进入命令行模式，而不启动Xserver。

如果想要恢复Xserver的启动模式，请使用如下命令：

    $echo “/usr/sbin/gdm” | sudo tee /etc/X11/default-display-manager

当然，也可以通过vi或者gedit来编辑 /etc/X11/default-display-manager以达到同样的效果。


##图形界面和命令行模式切换##

图形界面中按ctrl+f1-f7, f1-f6从图形界面进入命令行模式, f7从命令行模式进入图形界面。

命令行模式中执行，

gnome环境 $sudo /etc/init.d/gdm stop 

unity环境 $sudo /etc/init.d/lightdm stop

可以关掉Xserver，若要重新启动Xserver可以执行，

$startx

