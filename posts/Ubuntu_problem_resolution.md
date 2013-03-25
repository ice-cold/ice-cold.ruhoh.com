---
title: Ubuntu安装出现 The system is running in low-graphics mode解决方法
date: '2013-03-25'
description: Ubuntu安装或更新问题解决方法
categories: resolution
tags: [Ubuntu, 安装, 显卡驱动 ]
---

##Ubuntu更新出现 The system is running in low-graphics mode解决方法##

通常这种情况是由于ATI显卡引起的
按ctrl+alt+f1进行登录
这里要说明一下：在输入密码（password）的时候光标会闪烁，输入没反映，尽管输入就好了，输入完回车是一样的！
 
登录完之后输入以下：
sudo apt-get install fglrx
sudo reboot
