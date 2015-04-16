## 概述

每个包下面都有一个`package.json`文件，定义了这个项目所需要依赖的模块，以及项目的配置。

使用`npm install` 命令根据这个配置文件，自动下载所需的模块，也就是配置项目所需的运行和开发环境。

下面是一个的 package.json 文件示例

```bash
{
  "name": "startserver",
  "version": "1.0.6",
  "description": "Yet another http server",
  "keywords": ["server", "httpserver", "dev", "slider"],
  "main": "index.js",
  "bin": {
    "ss": "./bin/startserver",
    "startserver": "./bin/startserver"
  },
  "repository": {
    "type": "git",
    "url": "git://github.com/xudafeng/startserver.git"
  },
  "preferGlobal": true,
  "dependencies": {
    "foc": "~0.1.6",
    "ipv4": "0.0.4",
    "microtemplate": "~0.1.2",
    "marked": "~0.3.3",
    "highlight.js": "~8.3.0",
    "colorx": "0.0.5",
    "logx": "0.0.4",
    "ecmascript6": "~0.1.2",
    "commander": "~2.0.0",
    "co-request": "~0.2.0"
  },
  "devDependencies": {
    "ali.regenerator": "~0.4.12",
    "mocha": "*",
    "co-mocha": "~1.0.2",
    "istanbul-harmony": "~0.3.0",
    "should": "~4.0.4",
    "should-http": "~0.0.2",
    "jshint": "*"
  },
  "scripts": {
    "test": "make test",
    "jshint": "make jshint"
  },
  "precommit": [
    "jshint"
  ],
  "author": "xudafeng",
  "contributors": [
    "karoo",
    "ottomao",
    "meowtec"
  ],
  "email": "xudafeng@126.com",
  "blog": "http://xdf.me",
  "homepage": "http://startserver.github.io",
  "license": "MIT"
}

```

## scripts

scripts指定了运行脚本命令的npm命令行缩写，比如 test 指定了运行`npm run test`时，所要执行的命令。

## dependencies，devDependencies

dependencies和devDependencies指定了项目运行所依赖的模块和项目开发所需要的模块。

- **指定版本**：比如1.2.2，遵循“大版本.次要版本.小版本”的格式规定，安装时只安装指定版本。
- **波浪号（tilde）+指定版本**：比如~1.2.2，表示安装1.2.x的最新版本（不低于1.2.2），但是不安装1.3.x，也就是说安装时不改变大版本号和次要版本号。
- **插入号（caret）+指定版本**：比如&#710;1.2.2，表示安装1.x.x的最新版本（不低于1.2.2），但是不安装2.x.x，也就是说安装时不改变大版本号。需要注意的是，如果大版本号为0，则插入号的行为与波浪号相同，这是因为此时处于开发阶段，即使是次要版本号变动，也可能带来程序的不兼容。
- **latest**：安装最新版本。

`package.json` 文件可以手工编写，也可以使用`npm init`命令生成。


这个命令采用互动方式，要求用户回答一些问题，然后在当前目录生成一个基本的package.json文件。所有问题之中，只有项目名称（name）和项目版本（version）是必填的，其他都是选填的。

有了package.json文件，直接使用npm install命令，就会在当前目录中安装所需要的模块。

```bash
$ npm install

```

## bin

bin项用来指定各个内部命令对应的可执行文件的位置。

```js

"bin": {
  "startserver": "./bin/startserver."
}

```

上面代码指定，startserver 命令对应的可执行文件为 bin 子目录下的 startserver
文件。Npm会寻找这个文件，在`node_modules/.bin/`目录下建立符号链接。

## engines

engines 指定该项目所需要的`node.js`版本。

## preferGlobal

preferGlobal的值是布尔值，表示当用户不将该模块安装为全局模块时（即不用--global参数），要不要显示警告，表示该模块的本意就是安装为全局模块。

