---
title: Javascript 继承
date: 2015-04-10 16:50:46
tags: Javascript
categories: 编程
---

# 原型指针

```js
var a = new Array();
a.__proto__ === Array.prototype // true

a.__proto__.__proto__ === Object.prototype  // true

a.__proto__.__proto__.__proto__ === null  // true
```

# 原型对象

```js
var Foo = function() {}
Foo.__proto__ === Function.prototype // true

var a = new Foo();
a.__proto__ === Foo.prototype; // true

Foo.prototype.__proto__ === Object.prototype; // true

Foo.prototype.constructor === Foo; // true
a.constructor === Foo; // true
a.constructor === Foo.prototype.constructor; // true
```

# 原型链

利用原型让一个引用类型继承另一个引用类型的属性和方法

每个构造函数都有一个原型对象(prototype)，原型对象都包含一个指向构造函数的指针(constructor)，而实例都包含一个指向原型对象的内部指针(__proto__)

只需要让原型对象等于另一个类型的实例，此时的原型对象将包含一个指向另一个原型的指针，相应地，另一个原型中也包含着一个指向另一个构造函数的指针

当读取对象的某个属性时，JavaScript引擎先寻找对象本身的属性，如果找不到，就到它的原型去找，如果还是找不到，就到原型的原型去找。以此类推，如果直到最顶层的Object.prototype还是找不到，则返回undefine

![原型链](http://huang-jerryc.com/image/blog/philosophy-though-of-javascript-proto/289FC3BDCB0425AA1C9F0DC5EBA1079F.jpg)