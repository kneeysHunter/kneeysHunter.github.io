---
layout:     post
title:      limit order by
subtitle:   水滴石穿
date:       2020-10-14
author:     BY lxl
header-img: img/title/数据库权限.jpg
catalog: true
tags:
    - 数据库
---



## 1、任务描述

​    搜索表结构中的某些部分的数据，比如，最后面三个，最前面三个，第2到8条记录，等等。

## 2、实战演练

​    一、

> select * from tablename order by orderfield desc/asc limit position， counter；    
>
> position 指示从哪里开始查询，如果是0则是从头开始，counter 表示查询的个数    

> select * from tablename order by orderfield desc/asc limit 0,15

​    三、表示从3行以后开始(不包括第3行)，按照数据库顺序取10条数据.

>检索得到4到13行的数据。
>
> select * from auth_permission limit 3,10  (4-13)

​    四、LIMIT n 等价于 LIMIT **0**,n

>select  字段 from 表名 limit m offset n; 跳过前n行 取后面m行

##  limit 通常结合 order by使用

##  order by 用在where之后 用来对数据进行排序

![05SCSH.png](https://s1.ax1x.com/2020/10/14/05SCSH.png)

