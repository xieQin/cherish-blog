---
title: 使用nodejs搭建web服务器
date: 2015-07-25 13:52:41
tags: Nodejs
categories: Nodejs
---

搭建简单的web服务器

##### 服务器基本流程：
- 响应url请求，对应于硬盘上的文件
- 如果文件存在，返回200状态码，并发送文件到浏览器端
- 如果文件不存在，返回404状态码，并发送一个404文件到浏览器端
- 如果文件读取错误，返回500状态码，发送错误信息到浏览器端

##### 需要实现的基本功能点：
- 开启web服务，加载各种web资源
- 自动分配可用端口，也可以配置端口
- 加载json文件并模拟网速
- 启动时能自动打开默认浏览器浏览，方便调试
- 支持常用文件的MIME类型
- 允许跨域请求
- host默认为本地IP
- 可配置主页

##### 扩展功能
- 支持304缓存响应
- 启用GZip功能对指定文件进行压缩
- 支持断点续传
- 使用快捷命令

### 代码编写

##### 基本代码
```js
var http = require('http');        // Http服务器API
var fs = require('fs');            // 用于处理本地文件
var os = require('os');            //用于获取本地IP地址
var exec = require('child_process').exec; //用于打开默认浏览器
var path = require('path');     //用于处理路径和后缀
var url = require('url');       //用于解析get请求所带的参数

var CONFIG, //默认配置
    HTTP,   //HTTP静态类
    log;    //日志打印

CONFIG = {
  homedir:'',
  home: 'index.html',
  port: 8089,
  browser: true,
};
log = function(txt){ console.log(txt); };

HTTP = {
  init:function(){},
  _getIPAddress:function(){/* 获取本地IPv4的IP地址 */},
  _openURL:function(path){/* 使用默认浏览器打开URL */},
  _getMIME:function(ext){/* 获取文件的MIME类型 */},
  responseFile:function(pathName, res, ext, params){ /* 读取文件流并输出 */ }
  route:function( pathName, req, res ){/* 路由到指定的文件并响应输出 */},
  createServer:function(){/* 创建一个http服务 */},
  _bindEvents:function(server){ /* 注册响应事件 */};

HTTP.init();
```

##### 建立http服务
```js
var server = http.createServer();
server.listen(CONFIG.port!==0 ? CONFIG.port : 0);
```

##### 注册 监听端口 和 请求响应 
```js
var self = this, defaultUrl = CONFIG.homedir ? CONFIG.homedir+'/'+CONFIG.home : CONFIG.home;
// 注册监听端口启用事件
server.on('listening', function() { 
  var port = server.address().port;
  log('Server running at '+ port);
  CONFIG.browser && self._openURL('http://'+self._getIPAddress()+':'+port+'/'+defaultUrl);
})
```

##### 注册请求处理事件
```js
server.on('request', function(request, response) {
    // 解析请求的URL
    var oURL = url.parse(request.url);
    var pathName = oURL.pathname.slice(1);
    if(!pathName) pathName = defaultUrl;
    self.route.bind(self)(pathName, request, response);
});
```

##### 路由处理
```js
responseFile:function(pathName, res, ext, params){ /* 读取文件流并输出 */
  var self = this;
  var raw = fs.createReadStream(pathName);
  // 允许跨域调用
  res.setHeader("Access-Control-Allow-Origin", "*");
  res.setHeader("Content-Type", self._getMIME(ext));

  if(ext == 'json' && params.delay){
    setTimeout(function(){
      res.writeHead(200, "Ok");
      raw.pipe(res);
    },params.delay);
  }else{
    res.writeHead(200, "Ok");
    raw.pipe(res);
  }
},
route:function( pathName, req, res ){/* 路由到指定的文件并响应输出 */
  var self = this;
  fs.stat(pathName, function(err, stats){
    if(err){
      res.writeHead(404, "Not Found", {'Content-Type': 'text/plain'});
      res.write("This request URL " + pathName + " was not found on this server.");
      res.end();
    }else{
      if(stats.isDirectory()){
        pathName = path.join(pathName, '/', CONFIG.home);
        self.route(pathName, req, res);
      }else{
        var method = req.method,
            ext = path.extname(pathName), 
            params='';

        log(method+': '+pathName);// 打印请求日志

        ext = ext ? ext.slice(1) : 'unknown';

        // 如果是get请求，且url结尾为'/'，那么就返回 home 页
        if(method=='GET'){
          pathName.slice(-1) === '/' &&  (pathName = path.normalize(pathName + '/' +CONFIG.home));
          params = url.parse(req.url, true).query;
          self.responseFile.bind(self)(pathName, res, ext, params);
        }else if(method == 'POST'){
          var _postData = "", _postMap = "";
          req.on('data', function (chunk){
              _postData += chunk;
          }).on("end", function (){
            params = require('querystring').parse(_postData);
            responseFile.bind(self)(pathName, res, ext, params);
          });
        }else{
          self.responseFile.bind(self)(pathName, res, ext, params);
        }
      }
    }
  });
}
```