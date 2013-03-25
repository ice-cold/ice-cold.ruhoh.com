---
title: ubuntu12.04浏览器flash player插件安装
date: '2013-03-25'
description: ubuntu12.04浏览器flash player插件安装
categories: resolution
tags: [Ubuntu, 安装, flashplayer ]
---


ubuntu12.04给firefox,chrome装flash支持
flash插件下载地址: http://get.adobe.com/flashplayer/

下载tar.gz的就可以了

安装：

      tar xf  flash.tar.gz 
      sudo cp -r usr/* /usr
      sudo cp libflashplayer.so /usr/lib/firefox/plugins/

弄完两个浏览器就支持flash了
