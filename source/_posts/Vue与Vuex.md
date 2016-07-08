---
title: Vue与Vuex
date: 2016-03-25 12:59:18
tags: Vue
categories: Javascript
---

[vuex](https://github.com/vuejs/vuex)
[文档](http://vuex.vuejs.org/en/index.html)

# 总体流程
![总体流程](https://raw.githubusercontent.com/vuejs/vuex/master/docs/en/vuex.png)

# Demo
[quote-demo](https://github.com/xieQin/quote-demo)

# 学习总结
Vuex也是Flux的一种实现，是一个针对Vue特化的Flux，主要是为了配合Vue本身的响应式机制

相较于Redux，同样具有单状态树和热重载的api，不过也少了一些在Vue的场景下并不契合的特性，
如强制的immutability、为了同构而设计得较为繁琐的 API、必须依赖第三方库才能相对高效率地获得状态树的局部状态等

Vue + Vuex更为简洁，开发效率比React + Redux更高，更易于理解
