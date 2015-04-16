## 介绍

fs 是 filesystem 的缩写，该模块提供本地文件的 io 特性，也是 node
的最重要特性，它提供所有操作提供异步和同步两种操作方式，供开发者选择。

## readFileSync()

readFileSync方法用于同步读取文件，返回一个字符串。

```js
var fs = require('fs');

var data = fs.readFileSync(fileName, "utf8");
console.log(data);
```

该方法的第一个参数是文件路径，第二个参数是文本文件编码，默认为utf8。


## writeFileSync()

writeFileSync方法用于同步写入文件。

```js
var fs = require('fs');

var data = 'data';
fs.writeFileSync(fileName, data, 'utf8');
```

它的第一个参数是文件路径，第二个参数是写入文件的字符串，第三个参数是文件编码，默认为utf8。

## exists(path, callback)

exists方法用来判断给定路径是否存在，然后不管结果如何，都会调用回调函数。

```js
var fs = require('fs');

fs.exists(filePath, function (exists) {
  console.log(exists);
});
```

## mkdir()

mkdir方法用于新建目录。

```js
var fs = require('fs');

fs.mkdir(path, 0777, function(err) {
  if (err) {
    throw err;
  };
});

```

## writeFile方法用于写入文件。

```js
var fs = require('fs');

fs.writeFile('./helloDir/message.txt', 'Hello Node', function (err) {
  if (err) throw err;
  console.log('文件写入成功');
});

```

## readdir()

readdir方法用于读取目录，返回一个所包含的文件和子目录的数组。

```js
var fs = require('fs');

fs.readdir(process.cwd(), function(err, files) {
  if (err) {
    console.log(err);
    return;
  }

  console.log(files);
});

```

## stat()

stat方法的参数是一个文件或目录，它产生一个对象，该对象包含了该文件或目录的具体信息。我们往往通过该方法，判断正在处理的到底是一个文件，还是一个目录。

```js
var fs = require('fs');

fs.readdir('/etc/', function (err, files) {
  if (err) {
    throw err;
  };
  console.log(files);
});

```
