包管理篇
========

## npm 简介

npm 是 Node.js 的模块管理器，是一款命令行软件，用来安装和管理`node`模块。[官网](https://www.npmjs.com/)

npm 集成在 Node.js 安装包内，安装了 Node.js 就可以直接使用，一般不需要单独安装。

执行以下命令已确认环境中安装好 npm 无误。

```bash
$ npm -v
```

## npm 主要功能

- 下载三方模块
- 上传自己的模块

## 如何安装模块

```bash
$ npm install [package name]
$ npm install -g [package name]
```

模块可以`本地安装`，也可以`全局安装`。
两者的主要差异是模块在系统的位置和安装位置和调用方法。

`全局安装` 是将模块直接安装到 Node.js 全局环境中。
而`本地安装`是将模块下载到当前目录的 node_modules。

## 常用参数

安装命令可以使用不同参数，指定所安装的模块属于哪种依赖，效果主要体现在 `packages.json` 文件中。

```bash
--save：模块名将被添加到 dependencies
--save-dev: 模块名将被添加到 devDependencies
--save-optional：模块名将被添加到 optionalDependencies
```

## 如何调用

```js
var example = require('example');
```

## 如何更新

```bash
$ npm update [package name]
```

## 如何卸载

```bash
$ npm uninstall [package name]
```

## 如何发布自己的模块

```bash
$ npm publish [package name]
```

## 其他常用命令

```
$ npm help           # 显示命令
$ npm -l             # 显示常规用法
$ npm config list -l # 显示当前配置
```

## 源的概念



## package.json 概述

上面我们已经提及到了 `package.json`，不妨细说一下。
每个包下面都有一个`package.json`文件，定义了这个项目所需要依赖的模块，以及项目的配置。

`package.json` 文件可以手工编写，也可以使用`npm init`命令生成。

有了package.json文件，直接使用npm install命令，就会在当前目录中安装所需要的模块。

```bash
$ npm install

```

下面是一个的 `package.json` 文件示例

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

## bin

bin项用来指定各个内部命令对应的可执行文件的位置。

```js

"bin": {
  "startserver": "./bin/startserver"
}

```

上面代码指定，startserver 命令对应的可执行文件为 bin 子目录下的 startserver
文件。Npm会寻找这个文件，在`node_modules/.bin/`目录下建立软链接，就可以直接使用命令行启动了。

## main

main 字段制定了模块的入口文件，既整个模块的执行入口就是所指定的文件。

## scripts

scripts指定了运行脚本命令的 npm 命令行缩写，比如 test 指定了运行`npm run test`时，所要执行的命令。

## dependencies，devDependencies

dependencies 和 devDependencies 指定了项目运行所依赖的模块和项目开发所需要的模块。

- **指定版本**：比如1.2.2，遵循“大版本.次要版本.小版本”的格式规定，安装时只安装指定版本。
- **波浪号（tilde）+指定版本**：比如~1.2.2，表示安装1.2.x的最新版本（不低于1.2.2），但是不安装1.3.x，也就是说安装时不改变大版本号和次要版本号。
- **插入号（caret）+指定版本**：比如&#710;1.2.2，表示安装1.x.x的最新版本（不低于1.2.2），但是不安装2.x.x，也就是说安装时不改变大版本号。需要注意的是，如果大版本号为0，则插入号的行为与波浪号相同，这是因为此时处于开发阶段，即使是次要版本号变动，也可能带来程序的不兼容。
- **latest**：安装最新版本。

## engines

engines 指定该项目所需要的`node.js`版本。

## preferGlobal

preferGlobal 的值是布尔值，表示当用户不将该模块安装为全局模块时（即不用--global参数），要不要显示警告，表示该模块的本意就是安装为全局模块。
