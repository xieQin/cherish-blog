layout: es6
title: Generator函数
date: 2016-07-20 18:13:26
tags: Javascript
categories: 编程
---

## 基本语法
生成器函数返回一个生成器对象

```js
function* gen() {
    yield 1;
    yield 2;
    yield 3;
}
var g = gen();

console.log(g.next().value); //1
console.log(g.next().value); //2
console.log(g.next().value); //3
```
