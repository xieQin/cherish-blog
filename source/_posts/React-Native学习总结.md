---
title: React-Native学习总结
date: 2016-06-11 16:49:01
tags: React-Native
categories: React
---

[文档](https://facebook.github.io/react-native/docs/getting-started.html)

# 个人学习demo
[react-native-learning-starter](https://github.com/xieQin/react-native-learning-starter)

Android app

主要实现的功能：
- splash页
- 抽屉导航
- 带网络请求的ListView
- 界面切换及Android 返回按钮控制
- 下拉刷新

# 总体感受
如果只是用来实现简单的列表页+详情页，对于不熟悉Native开发的Web前端技术人员来说，React Native还是能很好地完成需求的，网络请求、UI视图交互、页面跳转均提供了很好的支持

但是如果需要使用PackageManager,ActivityManager等组件的话，就需要通过React Native和Native混合开发了
个人觉得对于实现复杂的应用来说，目前的RN社区还是缺乏一些高质量的组件，在找不到好用的组件的情况下，或者说大部分组件拿来后都要大修大改的情况下，实现 App 的效率其实非常低，大家都在忙着做一些基础的控件，很多东西都没有打磨好

# 环境配置及安装
依照[教程](https://facebook.github.io/react-native/docs/getting-started.html)安装即可
