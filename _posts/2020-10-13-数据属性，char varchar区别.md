---
layout:     post
title:      数据属性，char varchar 等
subtitle:   水滴石穿
date:       2020-10-13
author:     BY lxl
header-img: img/title/数据库权限.jpg
catalog: true
tags:
    - 数据库
---

#  数据属性

##  char （）与 varchar（）的区别

- char(n),n的范围为 1~255, varcher(n) n+1个字节 n范围为1~255

  - >varchar 会自动多一个字节用来储存数据长度
    >
    >```sql
    >char(5) 'a'-->char_length = 1
    >varchar(5)'a'-->char_length = 2
    >```

- char()，字符数 ，varchar（）字节数

  - char（）限制的是字符数，char(8）限制输入8个字符如 ‘李丽丽丽丽丽丽你’

  - varchar() 限制的是字节数，

    - >常见数据类型字节数 utf-8编码下
      >
      >int ,float , 4
      >
      >double ,8
      >
      >date 3,datetime 8,time 3, year 1.
      >
      >char 1,汉字 3

- char() 自动补全。varchar() 自动删除

  >type  带存储信息 存储信息   长度
  >
  >char(5)     'a'            'a    '		5
  >varchar(5)  'a    '      'a'			2

##  其他常见字段属性

- >primary key 主键，数据的唯一标示，不能重复
  >
  >- [主键，外键传送门](https://www.runoob.com/mysql/mysql-data-types.html)

- >not nulll 非空，输入数据时，该字段必需要写入

- >default 默认值。长配合not null使用

- >unique 唯一标识  使得该字段不能出现重复数据

- >comment 注释

  - 在desc tablename中可显示注释

- > unsigned 只能保存正数

- >date,datetime 时间属性 保存格式2020-01-20 16:44:55 长配合now()函数使用

- >enum 枚举 enum ('男'，'女') 只能是这两个中的数据，其他不接受报错