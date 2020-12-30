---
layout:     post
title:      Docker search 异常
subtitle:   Error response from daemon: Get https://index.docker.io/v1/search?q=ubuntu&n=25: x509: certificate has expired or is not yet valid
date:       2020-12-30
author:     BY lxl
header-img: img/title/数据库权限.jpg
catalog: true
tags:
    - Docker
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

##  docker search时出现<oooo>Error response from daemon</oooo>: Get https://index.docker.io/v1/search?q=ubuntu&n=25: x509: <oooo>certificate has expired or is not yet valid</oooo>

- 原因是系统时间不对
- ![rq6NOe.png](https://s3.ax1x.com/2020/12/30/rq6NOe.png)

### 解决

输入命令

```linux
 ntpdate cn.pool.ntp.org
```

- 即可

