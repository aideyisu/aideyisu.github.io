---
title: Linux三剑客-sed
top: false
cover: false
toc: true
mathjax: true
date: 2020-07-25 11:30:41
password:
summary:
tags:
categories:
---

## 介绍

三剑客威力巨大,各司其职.grep擅长查找;sed擅长取行和替换;awk擅长取列

#### sed 快速上手

##### 只是偶尔用一用

原文本
```shell
cat test_sed.txt
一楼有一个小朋友在吃苹果
二楼有一个高中生在边学习边吃苹果
三楼有一个老爷爷在用作业本学习
```

将全文的一个修改为两个
```shell
 sed s/一个/两个/g test_sed.txt
一楼有两个小朋友在吃苹果
二楼有两个高中生在边学习边吃苹果
三楼有两个老爷爷在用作业本学习
```
你可以发现和VIM的指令是一样的
s/原字符串/替换字符串/g

其中 /g代表全部匹配,如果没有/g只会修改匹配到的第一个选项
同时这并不会修改实际文件

#### 初步深入

##### 写出到文件

```shell
sed s/一个/两个/g test_sed.txt > delete.tx7ggjt
cat delete.txt
一楼有两个小朋友在吃苹果
二楼有两个高中生在边学习边吃苹果
三楼有两个老爷爷在用作业本学习
```

如上图所示我们就完成了一次输出重定向操作,将修改后的文件写到delete.txt中

##### 修改原文件

```
sed -i .tmp s/两个/一群/g delete.txt
cat delete.txt
一楼有一群小朋友在吃苹果
二楼有一群高中生在边学习边吃苹果
三楼有一群老爷爷在用作业本学习
```

此处mac与linux有一个区别
mac 强制在 -i 后需要选择一个备份文件
使用后delete.txt被修改,同时会生成delete.txt.tmp的原文件
linux无需制定 备份文件,那么在编写shell脚本时如何做普适性适配

```shell
if ["$(uname)" == "Darwin"];
    sed -i .tmp s...
    rm *.tmp
else
    sed -i s...
fi
```
如此对mac在shell脚本执行时做一个判定即可

##### 每行最前面引入

```shell
sed 's/^/# /g' test_sed.txt
# 一楼有一个小朋友在吃苹果
# 二楼有一个高中生在边学习边吃苹果
# 三楼有一个老爷爷在用作业本学习
```

此处mac有一个坑,需要声明
```shell
export LC_COLLATE='C'
export LC_CTYPE='C'
```
##### 每行最后面引入

```shell
sed 's/$/ [---] /g' test_sed.txt
一楼有一个小朋友在吃苹果 [---]
二楼有一个高中生在边学习边吃苹果 [---]
三楼有一个老爷爷在用作业本学习 [---]
```

#### 神奇的正则表达式

顺手介绍一下正则表达式的一些最基本的东西

| ^        | 表示一行的开头                          | /^#/ 以#开头的匹配        |
| $        | 表示一行的结尾                          | /}$/ 以}结尾的匹配        |
| \<       | 表示词首                                | \<abc 表示以 abc 为首的詞 |
| \>       | 表示词尾                                | abc\> 表示以 abc 結尾的詞 |
| .        | 表示任何单个字符                        |                           |
| *        | 表示某个字符出现了0次或多次             | --                        |
| [ ]      | 字符集合                                | [abc] 表示匹配a或b或c     |
| [a-zA-Z] | 表示匹配所有的26个字符如果其中有^表示反 | [^a] 表示非a的字符        |

