## 模块化

Node.js 采用模块化结构，按照[CommonJS规范](http://wiki.commonjs.org/wiki/CommonJS)定义和使用模块。模块与文件是一一对应关系，即加载一个模块，实际上就是加载对应的一个模块文件。

require方法用于指定加载模块。

```js
var a = require('a');
```

上面代码表明，从当前目录下的`a.js`文件，加载`a`模块。因为require方法默认加载的就是js文件，因此可以把js后缀名省略，所以也可以直接如下写法。

```js
var a = require('./a.js');
```

如果`require`方法的参数不带有路径，则`node.js`依次按照以下顺序，去寻找模块文件。
node.js依次到下面的目录，去寻找`a`模块。

```
- ./node_modules/a
- ../node_modules/a
- ../../node_modules/a
- /node_modules/a
```

可以看到，如果没有指明模块所在位置，Node会依次从当前目录向上，一级级在node_modules子目录下寻找模块。如果没有找到该模块，会抛出一个错误。这样做的好处是，不同的项目可以在自己的目录中，安装同一个模块的不同版本，而不会发生版本冲突。


## 核心模块

Node.js
本身还提供了一系列功能模块，与操作系统交互与调用。这些核心的功能模块集成在node中，可以直接使用。

- **http**：提供HTTP服务器功能。
- **url**：解析URL。
- **fs**：与文件系统交互。
- **querystring**：解析URL的查询字符串。
- **child_process**：新建子进程。
- **util**：提供一系列实用小工具。
- **path**：处理文件路径。

## 自定义模块

Node模块采用 CommonJS 规范。

下面是一个最简单的模块，假定新建一个`a.js`文件，写入以下内容。

```js

module.exports = function(i) {
  console.log(i);
};

```

上面代码就是一个模块，它通过module.exports变量，对外输出一个方法。

这个模块的使用方法如下。

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

## 异常处理

Node是单线程运行环境，一旦抛出的异常没有被捕获，就会引起整个进程的崩溃。所以，Node的异常处理对于保证系统的稳定运行非常重要。

### try-catch

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

### uncaughtException事件

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

### 全局对象和全局变量

Node提供以下几个全局对象，它们是所有模块都可以调用的。

- **global**：表示Node所在的全局环境，类似于浏览器的window对象。需要注意的是，如果在浏览器中声明一个全局变量，实际上是声明了一个全局对象的属性，比如`var x = 1`等同于设置`window.x = 1`，但是Node不是这样，至少在模块中不是这样（REPL环境的行为与浏览器一致）。在模块文件中，声明`var x = 1`，该变量不是`global`对象的属性，`global.x`等于undefined。这是因为模块的全局变量都是该模块私有的，其他模块无法取到。

- **process**：该对象表示Node所处的当前进程，允许开发者与该进程互动。
- **console**：指向Node内置的console模块，提供命令行环境中的标准输入、标准输出功能。
- **module**：该对象指向当前模块，`module.exports`属性是该模块对外的接口，被require方法调用。module实际上不是全局变量，而是每个模块私有的。
- **exports**：该对象指向`module.exports`属性，是该属性的简写形式。exports也不是全局变量，而是每个模块私有的。

Node还提供一些全局函数。

- **setTimeout()**：用于在指定毫秒之后，运行回调函数。实际的调用间隔，还取决于系统因素。间隔的毫秒数在1毫秒到2,147,483,647毫秒（约24.8天）之间。如果超过这个范围，会被自动改为1毫秒。该方法返回一个整数，代表这个新建定时器的编号。
- **clearTimeout()**：用于终止一个setTimeout方法新建的定时器。
- **setInterval()**：用于每隔一定毫秒调用回调函数。由于系统因素，可能无法保证每次调用之间正好间隔指定的毫秒数，但只会多于这个间隔，而不会少于它。指定的毫秒数必须是1到2,147,483,647（大约24.8天）之间的整数，如果超过这个范围，会被自动改为1毫秒。该方法返回一个整数，代表这个新建定时器的编号。
- **clearInterval()**：终止一个用setInterval方法新建的定时器。
- **require()**：用于加载模块。
- **Buffer()**：用于操作二进制数据。

Node提供两个全局变量。

- **__filename**：指向当前运行的脚本文件名。
- **__dirname**：指向当前运行的脚本所在的目录。

除此之外，还有一些对象实际上是模块内部的局部变量，指向的对象根据模块不同而不同，但是所有模块都适用，可以看作是伪全局变量，主要为module, module.exports, exports等。

module变量指代当前模块。module.exports变量表示当前模块对外输出的接口，其他文件加载该模块，实际上就是读取module.exports变量。

- module.id 模块的识别符，通常是模块的文件名。
- module.filename 模块的文件名。
- module.loaded 返回一个布尔值，表示模块是否已经完成加载。
- module.parent 返回使用该模块的模块。
- module.children 返回一个数组，表示该模块要用到的其他模块。
