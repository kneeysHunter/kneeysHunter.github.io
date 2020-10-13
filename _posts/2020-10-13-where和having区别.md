---
layout:     post
title:      where和having区别
subtitle:   try，哈
date:       2020-10-13
author:     BY lxl
header-img: img/title/数据库权限.jpg
catalog: true
tags:
    - 数据库
---

#  where 和  having区别

##  where 和having 都表示查询，大部分条件查询操作可以互换，除非一下几种情况

###  区别

- 使用角度

  >where 是一个约束声明，在查询数据库bai的结du果返回之前对数据库中的查询条件进行约束zhi，即在结果返回之前起作用

  >having是一个过滤声明，所谓过滤是在查询数据库的结果返回之后进行过滤，即在结果返回之后起作用

  ```sql
  select name age from teacher where id=1  --正确
  select name age from teacher having age=1  --正确
  对age进行了选取
  select name age from teacher having id=1  --错误
  因为having语句中并没有对id进行选取 
  ```

- where 语句可以在select update delete instert into 中使用 而having不可以

  >```sql 
  >delete from teacher where id=1 正确
  >delete from teacher having id=1 错误
  >```

- 使用别名时 where 不可以用别名作为条件，having则可以

  >```sql
  >select id as i,name as n from teacher where i=1 错误
  >select id as i,name as n from teacher having i=1 正确
  >```