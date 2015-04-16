## 异步操作

`Node.js`采用V8引擎处理，最大特点就是单线程运行。node
很多情况下采用异步操作（asynchronous opertion。这就导致，某一个任务的后续操作，往往采用回调函数（callback）的形式进行定义。

```js
var exampleFunction = function(callback) {
  ... do something
  callback();
}

var callback = function() {

}

exampleFunction(callback);
```

上面代码就把进一步的处理，交给回调函数callback。
