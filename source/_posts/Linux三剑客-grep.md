---
title: Linux三剑客-grep
top: false
cover: false
toc: true
mathjax: true
date: 2020-07-24 09:28:19
password:
summary:
tags:
categories:
---

## 介绍

三剑客威力巨大,各司其职.grep擅长查找;sed擅长取行和替换;awk擅长取列

## grep快速上手

#### 只是偶尔用一用

如果你不想仔细学习,日常学习只用一招完全够用..
```shell
cat test.py | grep def
    def searchInsert(self, nums: List[int], target: int) -> int:
```
会返回带有def的行,而且不需要任何参数,即开即用

#### 再多了解一点?

##### 最基本

第一条指令联合使用了 cat 和 grep 并不是非常优雅,那么标准用法是什么呢?
```shell
grep def test.py
    def searchInsert(self, nums: List[int], target: int) -> int:
```
可以看到直接 grep 查找内容 查找文件 就可以实现刚才两个指令才可以解决的问题

##### 查找文件内容中包含def的行数

```shell
grep -n def test.py
2:    def searchInsert(self, nums: List[int], target: int) -> int:
```
使用-n 参数即可完成任务

##### 不包含def的行

```shell
grep -v def test.py
class Solution:
        if(not nums):
            return 0
        n=len(nums)
        l=0
        r=n-1
        res=-1
        while(l<=r):
            mid=(l+r)//2
            if(nums[mid]==target):
                return mid
            elif(nums[mid]>target):
                r=mid-1
            else:
                l=mid+1
        res=l
        return res
```

此时可以看到测试文件的全文是一个leetcode题目

##### 查找以d开头的行

```shell
grep -n ^c test.py
1:class Solution:
```

##### 查找以冒号结尾的行

```shell
grep -n :$ test.py
1:class Solution:
2:    def searchInsert(self, nums: List[int], target: int) -> int:
3:        if(not nums):
9:        while(l<=r):
11:            if(nums[mid]==target):
13:            elif(nums[mid]>target):
15:            else:
```

可以看到所有以冒号结尾的行都会被显示出来

#### 继续深入探究

我们可以看到刚才用到了几个参数,那么全部参数都有什么呢

| 关键字        | 作用                    |
| ------------- | ----------------------- |
| --color=auto  | 对匹配到的文本着色处理  |
| -v            | 显示不被匹配到的行      |
| -i            | 忽略大小写              |
| -n            | 显示匹配到的行号        |
| -c            | 统计匹配的列数          |
| -o            | 仅显示匹配到的字符串    |
| -q            | 静默模式,不输出任何信息 |
| -A #          | after,后#行             |
| -B #          | before,前#行            |
| -C #          | context,前后各#行       |
| -e            | 实现多个选项间 或 关系  |
| -w            | 匹配整个单词            |
| -E            | 使用ERE,想当与egrep     |
| -F            | 相当于fgrep,不支持正则  |

灵活使用可以极大提升效率
其中 -v -n 应该会更实用一些

#### 结语

最近我弟中考完,也正在教他unity做个小游戏暑假
从2月疫情以来一直在教我弟,提升很明显,化学成绩从不及格弄到了全班第一(果然初中化学简单

在教我弟的过程我也在想如何更高效的学习,目前我的结论是,初期一定要看到一个小成果,就像玩游戏一样,一路上有一点激励会更能激发学习热情.一路吃苦,头悬梁锥刺股绝不是一般人的学习路径.

在这篇grep介绍中我参考了其他大佬的博客介绍方式,网上的课程
认为一篇这种文章编排,一定要让读者先看简明易懂的例子,看完马上就能用到工作中的那种

最后这种全部参数相对枯燥的东西,不适合一上来就看,应该看几个例子,对效率有一定提升后,可以带着更大的学习欲望来自己尝试全部参数的使用方法

这只是教一个初中生的过程的想法,可能不够完善,以后再有新的心得也会反思的

