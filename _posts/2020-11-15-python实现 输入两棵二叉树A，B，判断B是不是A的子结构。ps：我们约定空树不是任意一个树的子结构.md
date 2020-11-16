---
layout:     post
title:      python实现 输入两棵二叉树A，B，判断B是不是A的子结构。ps：我们约定空树不是任意一个树的子结构
subtitle:   python
date:       2020-11-15
author:     BY lxl
header-img: img/title/数据库权限.jpg
catalog: true
tags:
    - python
---

#   输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）

- return 与and和or的连用

  - return a and b  如果a返回true则执行b，否则不执行b。
  - return a or b  不论结果都会执行 a，b

- 思想：

  - 核心思想：对两个树在<em>第一个值相等</em>时进行相同的前序遍历（怎么遍历无所谓，只要满足顺序相同就行），如果满足

    1，两个树遍历的值相同，且b遍历完毕a还没有 则满足b是a的子树

    2，若a，b有一个不存在或者非空，不满足

    3，若遍历时a，b的值不同，不满足

- ***  第一个函数要每一种情况都进行判断，类似于滑块。***

```python
# -*- coding:utf-8 -*-
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Solution:
    def HasSubtree(self, pRoot1, pRoot2):
        # write code here
        if not pRoot1 or not pRoot2:
            return False
        return self.is_subtree(pRoot1, pRoot2) or self.HasSubtree(pRoot1.left, pRoot2) or self.HasSubtree(pRoot1.right, pRoot2)
      
    def is_subtree(self, A, B):
        if not B:
            return True
        if not A or A.val != B.val:
            return False
        return self.is_subtree(A.right, B.right) and self.is_subtree(A.left,B.left)
```

