## 异步操作

`Node.js`采用V8引擎处理，是单线程运行。node
很多情况下采用异步操作。某个操作的后续操作，一般采用回调函数的形式实现。

```js
var a = function(callback) {
  ... do something
  callback();
}

var callback = function() {

}

a(callback);
```

上面代码就把进一步的处理，交给回调函数callback。
