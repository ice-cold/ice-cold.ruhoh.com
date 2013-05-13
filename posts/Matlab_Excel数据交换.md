---
title: Matlab_Excel数据交换
date: '2013-05-13'
description: Matlab,Excel数据交换的几种方法
categories: matlab
tags: [matlab, excel ]
---

1. 常规：xlswrite与xlsread；

2. DDE：chann = ddeinit('excel','sheet1'); %(e.xls:sheet1)

range = 'r1c1:r20c20';

写数据 rc = ddepoke(chann,range,z); (注，动态数据交换时，此xls文件需要在Excel中已打开)

读数据 feature = dderep(chann, range);

3. excel link

**附：matlab颜色映像**

标准颜色映像

hsv,hot,cool,pink,gray,bone,jet,copper,prim,flag(都是64\*3矩阵).

以上映像函数接受一个参数来指定产生矩阵的行数，例如：hot(m)。

R  G  B

0  0  0  黑

1  1  1  白

1  0  0  红

0  1  0  绿

0  0  1  蓝

1  1  0  黄

1  0  1  洋红

0  1  1  青蓝

2/3  0  1  天蓝

1  1/2  0  橘黄

.5  0  0  深红

.5  .5  .5  灰
