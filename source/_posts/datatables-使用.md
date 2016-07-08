---
title: datatables 使用
date: 2014-08-12 18:29:56
tags: Jquery
categories: 插件
---

一款jQuery表格插件

[中文网](http://datatables.club/)
[文档](http://datatables.club/reference/)
[手册](http://datatables.club/manual/)

搭配ajax使用

```js
$(document).ready(function() {
  $('#example').dataTable( {
    "ajax": "data/objects.txt",
    "columns": [
      { "data": "name" },
      { "data": "position" },
      { "data": "office" },
      { "data": "extn" },
      { "data": "start_date" },
      { "data": "salary" }
    ]
  });
});
```

