---
title: 利用Sublime Text 2 来运行matlab
date: '2013-03-08'
description: Sublime Text 2文本编辑器中搭建MATLAB开发环境
categories: tool config
tags: [Sublime Text 2, Matlab ]
---

##搭建MATLAB开发环境##
Sublime Text 2文本编辑器中搭建MATLAB开发环境。当然，在Notepad++之类的编辑器上应该能以类似的方式实现。

**1.舍去笨重的GUI，以命令行的方式运行MALTAB**

Matlab能以命令行的方式运行（我打赌很多人都不知道），方法如下：

	点击开始，运行，输入cmd.exe进入命令行窗口

	输入 matlab -nosplash -nodesktop -r 文件名，即可运行脚本。注意，文件名是不包含.m后缀的，而且该m文件要么位于MATLAB的搜索路径中，要么得位于当前工作路径中。

其中，-nosplash关闭启动画面，-nodesktop关闭GUI（没有这项将打开完整的MATLAB界面），-r指的是运行(run)脚本，更详细的说明，请见：http://asc.2dark.org/node/111

**2.在Sublime Text下搭建MATLAB开发环境**

	新建Build System：点击Tool -> Build System -> New Build System，此时系统会自动新建一个JSON文件

	编辑这个JSON文件，将内容改为：{ "cmd": ["E:/MATLAB/R2012a/bin/matlab"(这里用你自己的路径), "-nosplash", "-nodesktop", "-r", "$file_base_name"], "selector": "source.m" }

	为这个JSON文件取个文件名保存（这个名字将成为新的Build System的名字，出现在Build菜单中）

	打开或新建一个.m文件，点击View -> Syntax -> open all with current extension as.. 在弹出的列表中选择MATLAB（这是因为Sublime Text 2目前会把.m文件当成Objective-C来自动设置语法高亮）

	设置完成。此时随便编辑一个MATLAB文件，在Build System下选择刚新建的配置，点击Tool -> Build，搞定。
