---
title: windows下安装DevKit
date: '2013-02-19'
description: 如何在windows下安装DevKit
categories: 软件安装
tags: [ruby, DevKit ]
---

##windows下安装或升级时gem经常会碰到##

1	Please update your PATH to include build tools or download the DevKit

2	from 'http://rubyinstaller.org/downloads' and follow the instructions

3	at 'http://github.com/oneclick/rubyinstaller/wiki/Development-Kit'

这是因为没有安装DevKit的缘故。

DevKit 是windows平台下编译和使用本地C/C++扩展包的工具。它就是用来模拟Linux平台下的make, gcc, sh来进行编译。注：这个方法目前仅支持通过RubyInstaller安装的Ruby，如果不是建议你重新安装。安装方法：双击下载的7z文件，指定解 压路径，路径中不能有空格。如C:\DevKit，这个路径就是<DEVKIT_INSTALL_DIR>。

1	> cd <DEVKIT_INSTALL_DIR>

2	> ruby dk.rb init

3	#生成config.yml，这里会检查将要添加DevKit支持的Ruby列表，只支持通过RubyInstaller安装的Ruby

4	#如果这里列出的Ruby与你的要求不符，可以手动修改

5	> ruby dk.rb review  #检查要添加DevKit支持的Ruby列表是否有误，可以略过

6	> ruby dk.rb install

7	[INFO] Updating convenience notice gem override for 'C:/Ruby192'

8	[INFO] Installing 'C:/Ruby192/lib/ruby/site_ruby/devkit.rb'

检查是否安装成功

1	> gem install rdiscount --platform=ruby

2	Fetching: rdiscount-1.6.8.gem (100%)

3	Temporarily enhancing PATH to include DevKit...

4	Building native extensions.  This could take a while...

5	Successfully installed rdiscount-1.6.8

6	1 gem installed

7	Installing ri documentation for rdiscount-1.6.8...

8	Installing RDoc documentation for rdiscount-1.6.8...

如果能安装rdiscount成功说明安装DevKit成功。

英文原版地址：https://github.com/oneclick/rubyinstaller/wiki/development-kit