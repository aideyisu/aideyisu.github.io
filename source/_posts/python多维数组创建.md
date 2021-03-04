---
title: python多维数组创建
top: false
cover: false
toc: true
mathjax: true
date: 2020-07-25 11:30:25
password:
summary:
tags:
categories:
---

## 起因

看到有行代码是这么写的

```python
n = 3
dp=[ [[0,0],[0,0],[0,0] ] for i in range(0,n) ]
```

我觉得可以简化 （查完资料发现是自己太菜了
```python
DP = [[[0] * 2] * 3 ] * n
```

写完之后原本美滋滋,但是试了试就完蛋了

```
dp[0][0][1] = 1
DP[0][0][1] = 1
```

两条看起来一样的指令但是结果完全不同

```
>>> dp
[[[0, 1], [0, 0], [0, 0]], [[0, 0], [0, 0], [0, 0]], [[0, 0], [0, 0], [0, 0]]]
>>> DP
[[[0, 1], [0, 1], [0, 1]], [[0, 1], [0, 1], [0, 1]], [[0, 1], [0, 1], [0, 1]]]
```


结果完全不一样,擦,查了查 [array] * 3 只是创建3个指向array的引用,一旦array发生改变,整个大数组都将发生改变...

以前都是好好写range的,今天突然想试试就遇到了
早就该遇到的,无非自己太菜现在才遇到=。=

## 创建方法

1 直接创建

```
Array = [[0,0,0], [0,0,0]]
```

2 列表生成法

``
Array = [[0 for i in range(m)] for j in range(n)]
```

3 numpy模块

```python
import numpy as np
Array = np.zeros((m, n), dtype=np.int)
```

