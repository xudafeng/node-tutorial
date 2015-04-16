web 编程
========

## http 模块

http 模块主要用于搭建HTTP服务。使用`Node.js`搭建HTTP服务器非常简单。

```js
var http = require('http');

http.createServer(function(request, response){
  response.writeHead(200, {'Content-Type': 'text/plain'});
  response.end('Hello World\n');
}).listen(8080, "127.0.0.1");

console.log('Server running on port 8080.');

```

上面代码第一行`var http = require("http")`，表示加载http模块。
然后，调用http模块的createServer方法，创造一个服务器实例。

`ceateServer`方法接受一个函数作为参数，该函数的request参数是一个对象，表示客户端的HTTP请求；response参数也是一个对象，表示服务器端的HTTP回应。response.writeHead方法表示，服务器端回应一个HTTP头信息；response.end方法表示，服务器端回应的具体内容，以及回应完成后关闭本次对话。最后的listen(8080)表示启动服务器实例，监听本机的8080端口。

将上面这几行代码保存成文件app.js，然后用node调用这个文件，服务器就开始运行了。

```bash
$ node app.js
```

回调函数的req（request）对象，拥有以下属性。

- url：发出请求的网址。
- method：HTTP 请求的方法。
- headers：HTTP 请求的所有 HTTP 头信息。

## POST请求

当客户端采用POST方法发送数据时，服务器端可以对`data`和`end`两个事件，设立监听函数。

```js

var http = require('http');

http.createServer(function(req, res) {
  var content = "";

  req.on('data', function(chunk) {
    content += chunk;
  });

  req.on('end', function() {
    res.writeHead(200, {"Content-Type": "text/plain"});
    res.write("You've sent: " + content);
    res.end();
  });

}).listen(8080);

```

data事件会在数据接收过程中，每收到一段数据就触发一次，接收到的数据被传入回调函数。end事件则是在所有数据接收完成后触发。

## get方法

get方法用于发出get请求。

```js

http.get({
  host: 'localhost',
  path: '/a'
}, function(response) {
  var body = '';
  response.on('data', function(d) {
    body += d;
  });

  response.on('end', function() {
    console.log(body);
  });
});

```

## request方法

request方法用于发出HTTP请求。

```js
var http = require('http');

var options = {
  host: 'www.baidu.com',
  path: '/'
};

var req = http.request(options, callback);

req.write("hello world!");
req.end();

```

request对象的第一个参数是options对象，用于指定请求的域名和路径，第二个参数是请求完成后的回调函数。

如果使用POST方法发出请求，只需在options对象中设定即可。

```js
var options = {
  host: 'www.example.com',
  path: '/',
  port: '80',
  method: 'POST'
};

```

指定 HTTP 头信息，也是在`options`对象中设定。

```js
var options = {
  headers: {
    custom: 'Custom Header Demo works'
  }
};

```

## 模块方法

 (1) http 模块的方法

- createServer(callback)：创造服务器实例。

 (2) 服务器实例的方法

- listen(port)：启动服务器监听指定端口。

 (3) HTTP回应的方法

- setHeader(key, value)：指定HTTP头信息。
- write(str)：指定HTTP回应的内容。
- end()：发送HTTP回应。

## koa 是什么？

致力于成为一个更小、更健壮、更富有表现力的 Web 框架。使用 koa 编写 web 应用，通过组合不同的 generator，可以免除重复繁琐的回调函数嵌套，并极大地提升常用错误处理效率。Koa 不在内核方法中绑定任何中间件，它仅仅提供了一个轻量优雅的函数库，使得编写 Web 应用变得得心应手。

```js
var koa = require('koa');
var app = koa();

// x-response-time
app.use(function *(next) {
  // (1) 进入路由
  var start = new Date;
  yield next;
  // (5) 再次进入 x-response-time 中间件，记录2次通过此中间件「穿越」的时间
  var ms = new Date - start;
  this.set('X-Response-Time', ms + 'ms');
  // (6) 返回 this.body
});

// logger
app.use(function *(next) {
  // (2) 进入 logger 中间件
  var start = new Date;
  yield next;
  // (4) 再次进入 logger 中间件，记录2次通过此中间件「穿越」的时间
  var ms = new Date - start;
  console.log('%s %s - %s', this.method, this.url, ms);
});

// response
app.use(function *() {
  // (3) 进入 response 中间件，没有捕获到下一个符合条件的中间件，传递到 upstream
  this.body = 'Hello World';
});

app.listen(3000);
```
