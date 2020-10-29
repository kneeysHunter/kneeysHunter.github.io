---
layout:     post
title:      leetcode 分糖果 只出现一次的数字
subtitle:   try，哈
date:       2020-10-28
author:     BY lxl
header-img: img/title/数据库权限.jpg
catalog: true
tags:
    - python
---



## 只出现一次的数字

[![B8kjns.png](https://s1.ax1x.com/2020/10/28/B8kjns.png)](https://imgchr.com/i/B8kjns)

##  使用异或

-  python 中异或符号为^ 

- 异或 （计算机存储整数的形式为为二进制）

  - 相同为0不同为1
  - 与0异或为自身
  - 3（0011）^ 4（0100） = 7（0111）
  - 异或符合交换律a^b^c=a^c^b

- 将序列中所有的数 一直异或下去 剩下的值就是出现一次的值，因为相同的异或为0（交换律）

  #   分水果

  

#  [![B8Zj2T.png](https://s1.ax1x.com/2020/10/28/B8Zj2T.png)](https://imgchr.com/i/B8Zj2T)

[![B8epqJ.png](https://s1.ax1x.com/2020/10/28/B8epqJ.png)](https://imgchr.com/i/B8epqJ)

```
1，想要拿到最小得，又必须有初始值 所以创建元素全为1，长度为输入列表长度的列表
2，要想分数高的小朋友要他比旁边得分低的小朋友分得的糖果多就分为两种情况
一种是分数高的在分数低的右边
一种是分数高的在分数低的左边
所以 for循环两次 判断条件都是前面的比后面的大（一次正序一次逆序）
因为第一遍循环已经有更改，所以第二次需要判断一下 列表中的数是大是小 大，则不变，小则加一
如不加判断 78965就会出错 因为第一遍循环之后9对应的值为3，已经比第二遍循环时6对应的值2高所以不需要加一
```