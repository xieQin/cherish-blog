---
title: Jquery源码阅读
date: 2015-08-21 14:25:18
tags: Jquery
categories: JavaScript
---
> jQuery 版本：2.0.3
> jQuery 源码学习笔记：

# 1. 整体架构

Jquey的核心是从HTML文档中匹配元素后执行操作
如：
>```js
 $(selector).append(html)
 $(selector).html(html).css()
```

具体步骤可分为:
- 构造jQuery对象

- 调用jQuery方法