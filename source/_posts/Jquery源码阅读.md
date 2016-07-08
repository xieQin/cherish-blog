---
title: jQuery源码阅读
date: 2015-08-21 14:25:18
tags: Jquery
categories: JavaScript
---
> jQuery 版本：2.0.3
> jQuery 源码学习笔记：
> [原文地址](http://www.cnblogs.com/aaronjs/p/3279314.html)

# 1. 整体架构

Jquey的核心是从HTML文档中匹配元素后执行操作
如：

```js
 $(selector).append(html)
 $(selector).html(html).css()
```

具体步骤可分为:
- 构造jQuery对象

- 调用jQuery方法

# 2. jQuery 构建

通过原型传递，把jQuery的原型传递给jQuery.prototype.init.prototype

```js
var jQuery = function(selector, context) {
 return  new aQuery.prototype.init();
}
jQuery.prototype = {
  init: function() {
    return this;
  },
  name: function() {
    return this.age
  },
  age: 20
}

jQuery.prototype.init.prototype = jQuery.prototype;

console.log(jQuery().name()) //20
```

# 3. 链式调用
实现链式的基本条件就是实例this的存在，并且是同一个

```js
jQuery.prototype = {
  init: function() {
    return this;
  },
  name: function() {
    return this
  }
}
```

```js
jQuery.init().name()
```

# 4. 插件接口
为jQuery或者jQuery prototype添加属性方法

jQuery.extend 对jQuery本身的属性和方法进行了扩展

jQuery.fn.extend 对jQuery.fn的属性和方法进行了扩展

jQuery.fn 是jQuery.prototype 的引用

```js
jQuery.extend = jQuery.fn.extend = function() {
}
```

# 5. 总结

- 通过new jQuery.fn.init() 构建一个新的对象，拥有init构造器的prototype原型对象的方法
- 通过改变prorotype指针的指向，让这个新的对象也指向了jQuery类的原型prototype