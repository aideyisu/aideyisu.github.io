---
title: Python二分查找内置库bisect
top: false
cover: false
toc: true
mathjax: true
date: 2020-07-05 19:33:01
password:
summary:
tags:
categories:
---

今天突然在网上看到的库，可以快速排序，叫做bisect
bisect模块实现了二分查找和插入算法，短小精干，简单易用

## 官方文档

我们首先来看看官方文档
This module provides support for maintaining a list in sorted order without having to sort the list after each insertion. For long lists of items with expensive comparison operations, this can be an improvement over the more common approach. The module is called bisect because it uses a basic bisection algorithm to do its work. The source code may be most useful as a working example of the algorithm (the boundary conditions are already right!).
重点:支持安排序顺序维护列表，使用二分查找方法提速，源码或许是最有用的工程算法实现(hhh官方吹捧
Ps - 使用此库前请保证list有序
Bisect 是二分法的意思，这里使用二分法来排序，它会将一个元素插入到一个有序列表的合适位置，这使得不需要每次调用 sort 的方式维护有序列表。

## 功能

bisect模块采用经典的二分算法查找元素。模块提供下面几个方法：
bisect.bisect_left(a, x, lo=0, hi=len(a))
定位x在序列a中的插入点，并保持原来的有序状态不变。参数lo和hi用于指定查找区间。如果x已经存在于a中，那么插入点在已存在元素的左边。函数的返回值是列表的整数下标。
bisect.bisect_right(a, x, lo=0, hi=len(a))
和上面的区别是插入点在右边。函数的返回值依然是一个列表下标整数。
bisect.bisect(a, x, lo=0, hi=len(a))
等同于bisect_right()。
注意，前面这三个方法都是获取插入位置，也就是列表的某个下标的，并不实际插入。但下面三个方法实际插入元素，没有返回值。
bisect.insort_left(a, x, lo=0, hi=len(a))
将x插入有序序列a内，并保持有序状态。相当于a.insert(bisect.bisect_left(a, x, lo, hi), x)。碰到相同的元素则插入到元素的左边。这个操作通常是 O(log n) 的时间复杂度。
bisect.insort_right(a, x, lo=0, hi=len(a))
同上，只不过碰到相同的元素则插入到元素的右边。
bisect.insort(a, x, lo=0, hi=len(a))
等同于insort_right()。

## 例子

官方文档中给出了一个简单实用例子和
利用利用bisect模块实现通用的列表元素查询方法的示范
文档链接：
https://docs.python.org/3/library/bisect.html
可以自行食用

## 结语

源码
https://github.com/python/cpython/blob/3.8/Lib/bisect.py
最近比较喜欢阅读官方文档和源码，很多教程写来写去也没说明白不如直接去看官方示例
所以除了最基本解释就不写了，大家可以直接看源码感受一下
