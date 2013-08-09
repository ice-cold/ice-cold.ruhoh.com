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

图形界面下的控制台切换 

crtl+alt+F1~F7

F1~F6是6个字符界面的控制台，F7返回图形界面控制台

命令行模式中执行，

    $sudo /etc/init.d/gdm stop #gnome环境
    $sudo /etc/init.d/lightdm stop #unity环境

可以关掉Xserver。Ubuntu12.04下字符界面启动图形界面：

    $startx
    
    
####背景知识####

*1、Ubuntu运行级别 * 

Linux 系统任何时候都运行在一个指定的运行级上，并且不同的运行级的程序和服务都不同，所要完成的工作和要达到的目的都不同，系统可以在这些运行级之间进行切换，以完成不同的工作。    
Ubuntu 的系统运行级别：

*0：关机级别   

*1：单用户运行级别，运行rc.sysinit和rc1.d目录下的脚本

*2：多用户，但系统不会启动NFS，字符模式，在有些linux系统中，级别2为默认模式，具有网络功能，如ubuntu.debian   

*3：多用户，字符模式，系统启动具有网络功能,redhat常用运行级别    

*4：用户自定义级别    

*5：图形界面模式，redhat常用运行级别  

*6：重启级别    

*S：单用户运行级别，只运行rc.sysinit文件    

*2、查看当前运行级别,执行命令：  *

runlevel  

（ runlevel 显示上次的运行级别和当前的运行级别，“N”表示没有上次的运行级别。）    

*3、切换运行级别，执行命令：  *   
int [0123456Ss]    

（ 即在 init 命令后跟一个参数，此参数是要切换到的运行级的运行级代号，如：用 init 0 命令关机；用 init 6 命令重新启动。）

