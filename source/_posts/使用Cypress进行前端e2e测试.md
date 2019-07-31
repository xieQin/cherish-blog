---
title: 使用Cypress进行前端e2e测试
date: 2019-07-12 12:59:18
tags: Cypress
categories: Test
---

[Cypress文档](https://docs.cypress.io/)

# e2e测试示例
[code-coverage](https://github.com/xieQin/code-coverage)

# Cypress概览
![总体流程](http://chuantu.xyz/t6/702/1564540539x2728309587.jpg)

# 编写测试用例总体流程
- 确定测试流程
- 明确流程中涉及到的元素及数据接口
- 使用data-cy标记元素
- 使用cy.get(), cy.route()进行数据接口mock
- 按功能需求编写用例
- 运行调试

# Cypress使用总结
### 优点
引入简单，开箱即用

官方示例多，利于开发与维护

gui 界面（ env：chrome 浏览器），可边测试边调整

截图功能，用例失败的场景节点会被截图保存，利于复现

自定义 fixture，可 mock 数据

自定义 commands，提高测试代码复用

支持单元测试

### 缺点
不支持兼容测试，只能运行在chrome环境中
