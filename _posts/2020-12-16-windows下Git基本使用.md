---
layout:     post
title:      git基本使用
subtitle:   git命令简单总结，以前都是使用github desktop版 ，想使用命令行，总结一下
date:       2020-12-16
author:     BY lxl
header-img: img/title/数据库权限.jpg
catalog: true
tags:
    - GIT
---

<style>
    oooo{
        color:red;
    }
</style>



<script src="https://eqcn.ajz.miesnfu.com/wp-content/plugins/wp-3d-pony/live2dw/lib/L2Dwidget.min.js"></script>

  <!--小帅哥：     https://unpkg.com/live2d-widget-model-chitose@1.0.5/assets/chitose.model.json-->
  <!--萌娘：       https://unpkg.com/live2d-widget-model-shizuku@1.0.5/assets/shizuku.model.json-->
  <!--小可爱（女）：https://unpkg.com/live2d-widget-model-koharu@1.0.5/assets/koharu.model.json-->
  <!--小可爱（男）：https://unpkg.com/live2d-widget-model-haruto@1.0.5/assets/haruto.model.json-->
  <!--初音：https://unpkg.com/live2d-widget-model-miku@1.0.5/assets/miku.model.json-->
   <!-- 上边的不同链接显示的是不同的小人，这个可以根据需要来选择 下边的初始化部分，可以修改宽高来修改小人的大小，或者是鼠标移动到小人上的透明度，也可以修改小人在页面出现的位置。 -->

<script>
    /*https://unpkg.com/live2d-widget-model-shizuku@1.0.5/assets/shizuku.model.json*/
    L2Dwidget.init({ "model": { jsonPath:
          "https://unpkg.com/live2d-widget-model-haruto@1.0.5/assets/haruto.model.json",
        "scale": 1 }, "display": { "position": "right", "width": 110, "height": 150,
        "hOffset": 0, "vOffset": -20 }, "mobile": { "show": true, "scale": 0.5 },
      "react": { "opacityDefault": 0.8, "opacityOnHover": 0.1 } });
</script>




#  Git 提交的使用基本流程

Git 是一个开源的分布式版本控制系统

![image-20210106122313919](C:\Users\39261\AppData\Roaming\Typora\typora-user-images\image-20210106122313919.png)

- 配置身份。
- git init创建仓库
- git add 将要想要提交的代码添加进来
- git commit 将添加进来的代码提交到（带备注）
- git push c 分支名称 将提交的代码进行同步

###  windows 请自行下载安装，https://git-scm.com/download/win安装成功右键会有git bash 提示

[![r1vPcn.png](https://s3.ax1x.com/2020/12/16/r1vPcn.png)](https://imgchr.com/i/r1vPcn)

###  1，首先配置自己的身份

```git
git config -global user.name "namexxx"
git config -global user.email "email@xxx"
```

- 查看身份

```git
git config --global user.name
git config --global user.email
```

###  2,创建仓库

- 进入本机的一个文件夹
- 输入命令

```git
git init
```

>此时该文件夹会出现一个<oooo>.git</oooo>文件表示这一个代码仓库，并在此记录所有的git信息，可以通过ls -a查看。

###  3，提交本地代码

- ```git
  git add <filename>
  ```

  将想要提交的代码添加进来

- ```git
  git add <dirname>
  ```

  添加的整个目录

- ```git 
  git add .
  ```

  将所有的都添加进去，所有的是指与原来不同的或有修改的地方

- ```git
  git commit -m"备注信息"
  ```

<oooo>注意此时文件备注不可省略</oooo>

- ```git
  git push origin <分支名称>
  ```

##  查看修改内容

- ```git
  git status
  ```

  查看上次 修改过的文件

- ```git
  git diff 
  ```

  查看当前仓库中那些文件做了更改，以及更改的内容 

  ```git
  git diff <filename>
  ```

  查看指定指定文件做了什么改动（文件名为其绝对路径）

##  查看修改日志

- ```git 
  git log
  ```

  显示提交id，提交人，提交日期，提交描述

  [![r1OSh9.png](https://s3.ax1x.com/2020/12/16/r1OSh9.png)](https://imgchr.com/i/r1OSh9)

##  分支

[![r1vPcn.png](https://s3.ax1x.com/2020/12/16/r1vPcn.png)](https://imgchr.com/i/r1vPcn)

[![r1vMcR.png](https://s3.ax1x.com/2020/12/16/r1vMcR.png)](https://imgchr.com/i/r1vMcR)

- ```git
  git branch  <分支名称>
  ```

  在当前分支上建立新分支

- ```git 
  git branch 
  ```

  查看所有分支

- ```git
  git checkout <分支名称>
  ```

  切换分支

###  <oooo>使用git提交代码到github</oooo>

演示以新创仓库为例

- 创建一个本地文件夹作为自己的仓库

- 右键 git bash here

- ```git
  git init 
  ```

  将此文件夹作文git仓库，此时会多一个.git文件

  [![r1ztld.png](https://s3.ax1x.com/2020/12/16/r1ztld.png)](https://imgchr.com/i/r1ztld)

- ```
  git remote add origin "仓库地址"
  ```

  将本地仓库绑定到github仓库上

  [![r3gYjA.png](https://s3.ax1x.com/2020/12/17/r3gYjA.png)](https://imgchr.com/i/r3gYjA)

- ```git
  ssh-keygen -t rsa -C "绑定的邮箱"
  ```

  **生成本机的<oooo>ssh key 密钥</oooo>作为连接凭证**

  - ```git
    cat ~/.ssh/id_rsa.pub
    ```

    **查看密钥**

    [![r32fsA.png](https://s3.ax1x.com/2020/12/17/r32fsA.png)](https://imgchr.com/i/r32fsA)

  <oooo>一个人的本机仓库有很多，但本机的ssh key只需要一个</oooo>

- 将获取的ssh密钥添加到github仓库允许的ssh连接上

  [![r3gICF.png](https://s3.ax1x.com/2020/12/17/r3gICF.png)](https://imgchr.com/i/r3gICF)

  [![r3gG1H.png](https://s3.ax1x.com/2020/12/17/r3gG1H.png)](https://imgchr.com/i/r3gG1H)

  

- 提交步骤，即可

  ```git
  git add .
  git commit -m"xxx"
  git pull origin master(自己的分支名)
  ```

  #  可能出现的问题

  ## 初次push出现登录的问题

  - ```git
    git push -u origin master
    ```

    弹出的登录用户名和密码等。。

    <oooo>报错remote: Invalid username or password，fatal: Authentication failed for 'https:/github....</oooo>

  - 原因：此时输入的账户和密码并不是 github的账号 用户名和密码而是

    **而是GitHub的Personal access tokens**

    

  [![r1xaIU.png](https://s3.ax1x.com/2020/12/16/r1xaIU.png)](https://imgchr.com/i/r1xaIU)
  ![r1xGMn.png](https://s3.ax1x.com/2020/12/16/r1xGMn.png)
  ![r1x12j.png](https://s3.ax1x.com/2020/12/16/r1x12j.png)

  ##  若出现 fatal: remote origin already exists.

  


  ![r3Wkh8.png](https://s3.ax1x.com/2020/12/17/r3Wkh8.png)

第一句报错：
fatal: remote origin already exists.
远程起源已经存在。

第二句报错：
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.
git@github.com：权限被拒绝（publickey）。
致命：无法从远程存储库读取。

第三句报错：
Please make sure you have the correct access rights
and the repository exists.
请确保您拥有正确的访问权限
并且存储库存在。

**原因是没有ssh连接认证** 使得

```git
git remote add origin "xxx"
```

之后无法提交，解决方法 ssh认证 上面有

##  出现fatal: refusing to merge unrelated histories解决方法。

###  出现问题：不同本地仓库（文件夹）向同一个git 仓库里面提交代码。

###  问题原因：两个项目不同。git默认不允许不同的项目合并。

###  解决方法：

添加：

```git
--allow-unrelated-histories
```

允许不相关的历史合并。

例如：

```git
git push origin master --allow-unrelated-histories
```

##  无法push到仓库，多数需要先进行同步，先pull，在push

#  Git 分支

### 分支

分支（branch）有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

### 分支内部原理

1、如下图所示，版本的每一次提交（commit），git都将它们根据提交的时间点串联成一条线。刚开始是只有一条时间线，即master分支，HEAD指向的是当前分支的当前版本。

 ![img](https://img-blog.csdn.net/20160122230457471)

2、当创建了新分支，比如dev分支（通过命令git branch dev完成），git新建一个指针dev，dev=master，dev指向master指向的版本，然后切换到dev分支（通过命令git checkout dev完成），把HEAD指针指向dev，如下图。

![img](https://img-blog.csdn.net/20160122231232795)

3、在dev分支上编码开发时，都是在dev上进行指针移动，比如在dev分支上commit一次，dev指针往前移动一步，但是master指针没有变，如下：

![img](https://img-blog.csdn.net/20160122231356422)

4、当我们完成了dev分支上的工作，要进行分支合并，把dev分支的内容合并到master分支上（通过首先切换到master分支，git branch master，然后合并git merge dev命令完成）。其内部的原理，其实就是先把HEAD指针指向master，再把master指针指向现在的dev指针指向的内容。如下图。

![img](https://img-blog.csdn.net/20160122231702926)

5、当合并分支的时候出现冲突（confict），比如在dev分支上commit了一个文件file1，同时在master分支上也提交了该文件file1，修改的地方不同（比如都修改了同一个语句），那么合并的时候就有可能出现冲突，如下图所示。

![img](https://img-blog.csdn.net/20160122233146679)

这时候执行git merge dev命令，git会默认执行合并，但是要手动解决下冲突，然后在master上git add并且git commit，现在git分支的结构如下图。

![img](https://img-blog.csdn.net/20160122233448030)

可以使用如下命令查看分支合并情况。



1. git log --graph --pretty=oneline --abbrev-commit 



6、合并完成后，就可以删除掉dev分支（通过git branch -d dev命令完成）。

![img](https://img-blog.csdn.net/20160122231752833)



如此，就是分支开发的原理。其好处也是显而易见的。