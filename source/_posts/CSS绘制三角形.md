---
title: CSS绘制三角形
date: 2014-12-21 11:18:12
tags: CSS
categories: 前端
---

CSS绘制三角形是对border属性的应用

```html
<div class="test"></div>
```

```css
.test{
  width: 0;
  height: 0;
  border-top: 50px solid black;
  border-right: 50px solid red;
  border-bottom: 50px solid blue;
  border-left: 50px solid orange;
}
```

![效果](https://segmentfault.com/img/bVlP6n)

绘制各种三角形：
必须设置三个边框的，且位于两侧的边框的 border-color 属性应设置为 transparent

```css
.test1{
  width: 0;
  height: 0;
  border-right: 50px solid transparent;
  border-bottom: 50px solid blue;
  border-left: 50px solid transparent;
}
.test2{
  width: 0;
  height: 0;
  border-top: 50px solid transparent;
  border-bottom: 50px solid transparent;
  border-left: 50px solid orange;
}
.test3{
  width: 0;
  height: 0;
  border-top: 50px solid black;
  border-right: 50px solid transparent;
  border-left: 50px solid transparent;
}
.test4{
  width: 0;
  height: 0;
  border-top: 50px solid transparent;
  border-right: 50px solid red;
  border-bottom: 50px solid transparent;
}
```