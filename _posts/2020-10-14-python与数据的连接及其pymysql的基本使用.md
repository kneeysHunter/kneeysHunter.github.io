---
layout:     post
title:      pymysql的连接与使用
subtitle:   try，哈
date:       2020-10-14
author:     BY lxl
header-img: img/title/数据库权限.jpg
catalog: true
tags:
    - 数据库
---

## pymysql的基本使用

- >安装pymysql第三方库

  ```python
  pip install pymysql
  ```

  

- >1,连接数据库

  ```python
  db = pymysql.connect(
  host = '你的数据库地址',
  user = '你的数据库用户'
  password = '你的用户密码'
  charset='utf8'#编码格式
  port=3306#端口号 一般默认3306 （阿里云需要自己手动打开）
  )
  #connect用来返回建立代码与书库连接的对象db，
  ```

  <strong>需要最后进行关闭db.close()<strong>

  - 

    > connect = Connection = Connect三个用来创建对象都可以，效果一样

    >- 参数host：连接的mysql主机，如果本机是’localhost’
    >- 参数port：连接的mysql主机的端口，默认是3306
    >- 参数database：数据库的名称
    >- 参数user：连接的用户名
    >- 参数password：连接的密码
    >- 参数charset：通信采用的编码方式，推荐使用utf8
    >  3.关闭连接 conn.close()

- >2,创建可以执行sql语句的游标对象

  ```python
  cursor = db.cursor()
  ```

- <strong>需要最后进行关闭cursor.close()<strong>

- 

  >3,执行sql语句
  >
  >```python
  >cursor.execute(sql,args)
  >```

  >- 若sql只需要一个参数，可以直接写
  >
  >```python
  >sql = 'insert into t_student(grade) value(%s)'
  >c = cursor.execute(sql,1001)
  >```

  >- 若sql需要两个参数，则传入的参数必需以元组形式

  ```python
  sql = 'insert into t_student(studentName,grade) value(%s,%s)'
  c = cursor.execute(sql,('李晓亮',1001))
  ```

  

- 若多个插入 使用executemany(sql,args)函数

  >```python
  >sql = 'insert into t_student(studentName,grade) value(%s,%s)'
  >c = cursor.executemany(sql,[('李晓亮',1001),('李晓亮',1010)])
  >```

  - 参数外层是一个列表，里面是元组，<strong>列表的长度就是重复的次数<strong>

    里面的元组是每次传递的参数，

    ```python
    c = cursor.executemany(sql,[('李晓亮',1001),('李晓亮',1010)])
    #重复两次
    c = cursor.executemany(sql,[('李晓亮',1001),('李晓亮',1010)，('李晓亮',1010)])
    #重复三次
    ```

- 获取结果集中的一条 cur.fetchone() 返回一个元组 如 (1,‘妲己’,18)

  获取结果集中的一条 cur.fetchmany(2) 返回一个元组 如 ((1,‘妲己’,18),2,‘公孙离’,20)）

  获取结果集中的所有 cur.fetchall() 执行查询时，获取结果集的所有行，一行构成一个元组，再将这些元组装入一个元组返回. 如((1,‘妲己’,18),（2,‘公孙离’,20),(3,‘姜子牙’,28))

<p style="font-size:30px">db.commit()提交语句，在增删改中。执行此语句提交到数据库，进行同步。</p>

