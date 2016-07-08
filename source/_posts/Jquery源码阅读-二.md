---
title: jQuery源码阅读(二)
date: 2015-08-30 17:27:53
tags:
---
> jQuery 版本：2.0.3
> jQuery 源码学习笔记（二）：
> [原文地址](http://www.cnblogs.com/aaronjs/p/3279314.html)

# 事件绑定

## 1. 事件绑定接口

![事件绑定接口](http://images.cnitblog.com/blog/329084/201311/25131537-e46635f5fd144ceeb43c1bf8d3516dfc.png)

jQuery的事件绑定，以click方法为例：
- click
- bind
- delegate
- on

## 2. jQuery事件流程图

![jQuery事件流程图](http://images.cnitblog.com/blog/329084/201311/26084505-ee141e573a864f148af28f3cf62b6196.png)