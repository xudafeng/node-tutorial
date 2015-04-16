进阶篇
======

## 模块化

Node.js 采用模块化结构，遵照[CommonJS规范](http://wiki.commonjs.org/wiki/CommonJS)的定义和使用。模块与文件是一一对应的。加载一个模块，实际上就是加载对应的一个模块文件。

require方法用于指定加载模块。

```js
var a = require('a');
```

上面代码表明，以当前目录下的`a.js`文件为路径，加载名为`a`的模块。由于 require
方法默认加载后缀为`.js`的文件，因此可以把后缀省略，所以也可以直接如下写法。

```js
var a = require('./a');
```

如果`require`方法的参数不带有路径，则`node.js`依次按照以下顺序，去寻找模块文件。
node.js依次到下面的目录，去寻找`a`模块。

```bash
- ./node_modules/a
- ../node_modules/a
- ../../node_modules/a
- /node_modules/a
```

Node会依次从当前目录向上，一级级在`node_modules`子目录下寻找模块。如果没有找到该模块，会抛出一个错误。这样做的好处是，不同的项目可以在自己的目录中，安装同一个模块的不同版本，而不会发生版本冲突。

## 系统模块

Node.js 系统提供了一系列功能模块，与操作系统交互与调用。这些核心的功能模块集成在 node 中，可以直接使用。

- **http**：HTTP 相关功能。
- **path**：处理文件路径。
- **url**：操作 URL。
- **fs**：系统 io 功能。
- **child_process**：进程功能。
- **util**：提供了一些工具。

## 自定义模块

下面是一个最简单的模块，新建一个`a.js`文件如下：

```js
module.exports = function(i) {
  console.log(i);
};

```

上面代码就是一个模块，它通过`module.exports`变量，对外输出一个方法。

使用方法如下:

```js
var m = require('./a');
m('输出');
```

更深入的用法：

```js
function doSomething(i) {
  console.log(i);
}

function a(i) {
  doSomething(i);
}

module.exports = a;
```

## 全局对象和全局变量

Node提供以下几个全局对象

- **global**：global 为 node 全局对象。
- **process**：该对象表示 Node 所处的当前进程，允许与此进程交互。
- **console**：这是 Node 内置的 console 模块，提供命令行环境中的输出。
- **module**：该对象指向当前模块，`module.exports`属性是该模块对外的接口，被require方法调用。
- **exports**：该对象指向`module.exports`属性，是该属性的简写形式。exports也不是全局变量，而是每个模块私有的。

Node 提供一些全局函数。

- **setTimeout()**：提供简单的定时器功能。
- **clearTimeout()**：用于终止一个 setTimeout 方法新建的定时器。
- **setInterval()**：循环定时器。
- **clearInterval()**：终止一个用 setInterval 方法新建的定时器。
- **require()**：用于加载模块。
- **Buffer()**：用于操作二进制数据。

Node提供两个全局变量。

- **__filename**：获取当前运行的脚本文件名。
- **__dirname**：获取当前运行的脚本所在的目录名。

module变量指代当前模块。module.exports 变量表示当前模块对外输出的接口，其他文件加载该模块，实际上就是读取 module.exports 变量。

- module.id 模块的识别符，通常是模块的文件名。
- module.filename 模块的文件名。
- module.loaded 返回一个布尔值，表示模块是否已经完成加载。
- module.parent 返回使用该模块的模块。
- module.children 返回一个数组，表示该模块要用到的其他模块。

## 异常处理

## try-catch

最常用的捕获异常的方式，就是使用try...catch。但是却无法捕获异步运行的代码抛出的异常。

```js

try {
  setTimeout(function(){
    throw new Error("error");
  }, 16);
} catch(err) {
  console.log(err);
}

```

代码抛出的异常无法被 catch 代码块捕获。

怎么办？

## uncaughtException事件

当一个异常未被捕获，就会触发 uncaughtException 事件，可以对这个事件注册回调函数，从而捕获异常。

```js
process.on('uncaughtException', function(err) {
  console.error('Error caught in uncaughtException event:', err);
});

try {
  setTimeout(function(){
    throw new Error("error");
  }, 16);
} catch (err) {
  console.log(err);
}

```
