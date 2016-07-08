---
title: CommonJs、AMD、UMD
date: 2015-11-30 17:56:11
tags: Javascript
categories: 前端
---
js的模块化方案真是层出不穷，专门记录一下各个方案之间的差别

[参考文章](http://davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/)

### 一、AMD
异步模块定义，专门为浏览器中js环境设计的规范
requirejs的模块化方案，在用requirejs做项目的时候接触到的

基本api:

```js
define(id?, dependencies?, factory);
```

定义无依赖的模块：

```js
define(function() {
  return {
    mix: function(source, target) {
    }
  };
});
````

定义有依赖的模块：

```js
define(['base'], function(base) {
    return {
        show: function() {
            // todo with module base
        }
    }
});

define(['data', 'ui'], function(data, ui) {
    // init here
});
```

定义数据对象模块:

```js
define({
    users: [],
    members: []
});
```

### 二、Commonjs
一个单独的文件就是一个模块
每一个模块都是一个单独的作用域，在一个文件定义的变量（还包括函数和类），都是私有的

CommonJS定义的模块分为:
  - 模块引用(require)
  - 模块定义(exports)
  - 模块标识(module)

```js
// foo.js
var request = require('request').default({ 
    timeout: 4000
});

module.exports = function(){ 
    this.re = '';
    this.req = function(url){ 
        request(url,function(error,status,res){ 
            this.re = res;
        });
    }
};
```

```js
// main.js

var Foo = require('./foo');
var foo = new Foo();
foo.req('http://www.baidu.com');
console.log(foo.re);
```

CommonJS 加载模块是同步的，所以只有加载完成才能执行后面的操作

### 三、UMD

UMD是AMD和CommonJS的糅合

UMD先判断是否支持Node.js的模块（exports）是否存在，存在则使用Node.js模块模式。
再判断是否支持AMD（define是否存在），存在则使用AMD方式加载模块
