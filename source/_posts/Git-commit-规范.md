---
title: Git commit 规范
top: false
cover: false
toc: true
mathjax: true
date: 2020-05-16 22:02:18
password:
summary:
tags:
categories:
---

## 背景:

    Git毫无疑问是现在最流行的版本控制工具。在回顾项目，定位问题的过程中，书写良好的commit message可以提高效率~♪（＾∀＾●）ﾉｼ写这个也是自己的备忘录～

## 规范?直接上手！

#### type

type为必填项，用于指定commit的类型，约定了feat、fix两个主要type，以及docs、style、build、refactor、revert五个特殊type，其余type暂不使用。

###### 主要type

| 名称  | 解释           |
| ----- | -------------- |
| feat  |     增加新功能 |
| fix   |    修复bug     |

###### 特殊type

| 名称  | 解释           |
| ----- | -------------- |
| docs     |     只改动了文档相关的内容                                |
| style    |    不影响代码含义的改动，例如去掉空格、改变缩进、增删分号 |
| build    |    构造工具的或者外部依赖的改动，例如webpack，npm         |
| refactor | 代码重构时使用                                            |
| revert   |   执行git revert打印的message                             |

###### 暂不使用type

| 名称  | 解释           |
| ----- | -------------- |
| test  |     添加测试或者修改现有测试                                 |
| perf  |     提高性能的改动                                           |
| ci    |       与CI（持续集成服务）有关的改动                         |
| chore |    不修改src或者test的其余修改，例如构建过程或辅助工具的变动 |

###### 注意事项

当一次改动包括主要type与特殊type时，统一采用主要type

#### 最后

我现在更喜欢commit干练即可
等到提合并请求时再详细写明原因
