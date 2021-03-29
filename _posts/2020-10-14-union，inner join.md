---
layout:     post
title:      union inner/left/right join
date:       2020-11-30
author:     BY lxl
header-img: img/title/数据库权限.jpg
catalog: true
tags:
    - 数据库
---



##  union(数据拼接要求列相等)

- union 会去掉重复，union all 显示重复

>```sql
>select * from teacher union select * from student
>```
>
>将student的数据拼接到<strong>teacher<strong>下面。要求teacher和student表中列数相等

### 在表一中的字段 表二没有，union拼接时，表二的元素会自动拼接到表一下，失去原有字段名



- 若两个表的列数不相等，则选择相等数量的字段

只写字段名，union中独有

>```sql
>select id ,name,age from teacher union select grade,score,name from student
>```

正常写法

>```sql
>select teacher.id,teacher.age from teacher union student.grade,student.age from student;
>```

##  inner join （交集作为条件拼接 ）

>- 字段必须标示表名，因为两个表可能有相同字段，不知道选取那个。如果不写表名也可能会正确，因为该字段只在一个表中
>
>在 teacher表和student表中选择
>
>```sql
>select teacher.id ,teacher.age,student.grade from teacher inner join student on teacher.id=student.id
>```
>
>选取teacher表中id与student表中id相等的：teacher表中的id ，age字段student中的grade字段 

- on后面跟 交集条件

##  left join （左边表中的都有 ）

>left join 左边表中的都有，加上右边表的交集数据
>
>```sql
>select teacher.*,student.age,student.name from teacher left join student on 
>student.id=teacher.id
>在teacher表中的所有数据都会被取出，id不相等的 拼接时自动填写null
>```
>
>![05KqeK.png](https://s1.ax1x.com/2020/10/14/05KqeK.png)

![05KvJH.png](https://s1.ax1x.com/2020/10/14/05KvJH.png)

##  right join 同上