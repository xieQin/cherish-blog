---
title: Javascript事件
date: 2016-06-07 10:16:30
tags: Javascript
categories: 编程
---

## 1. 事件流
事件流描述的是从页面中接收事件的顺序

#### 1.1 事件冒泡
IE的事件流：事件冒泡（event bubbling），即事件开始时由最具体的元素（文档中嵌套层次最深的那个节点）接收，然后逐级向上传播到较为不具体的节点（文档）

```html
<!DOCTYPE html>
<html>
<head>
  <title>Event Bubbling Example</title>
</head>
<body>
  <div id="myDiv">Click Me</div>
</body>
</html>
```
点击页面中的`<div>`元素，那么click事件会按照如下顺序传播：
1. `<div>`
2. `<body>`
3. `<html>`
4. `document`

#### 1.2 事件捕获
事件捕获的思想是不太具体的节点应该更早接收到事件，而最具体的节点应该最后接收到事件。
事件捕获的用意在于在事件到达预定目标之前捕获它。

点击页面中的`<div>`元素，click事件会按照如下顺序传播：
1. `document`
2. `<html>`
3. `<body>`
4. `<div>`

#### 1.2 DOM事件流
“DOM2级事件”规定的事件流包括三个阶段：事件捕获阶段、处于目标阶段和事件冒泡阶段

![Alt text](http://img1.zsgjs.com/upfile/file/2016/0615/7644326177bdc141c1b2b85d4575d528.png)

## 2. 事件处理程序
响应某个事件的函数就是事件处理程序，或事件侦听器

#### 2.1 HTML事件处理程序
```html
<input type="button" name="btn" onclick="alert('Clicked')" value="Click Me" />
```

#### 2.2 DOM 0级事件处理程序
