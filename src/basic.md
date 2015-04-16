基础篇
======

## Nodejs 是什么？

Node.js 诞生于 2009 年，是 JavaScript 在服务器端的一个运行环境。它的 JavaScript
解释器，采用了Google 公司的 V8
引擎。主要用于方便地搭建响应速度快、易于扩展的网络应用。Node.js
使用事件驱动，非阻塞I/O 模型使其轻量和高效。

## io.js

io.js 是一个衍生自 Node.js™，并兼容 npm 的开发平台，更完美地支持
ES6。提升了系统的性能，额外支持 ES6
语言特性，提升了所有平台的性能和稳定性。

了解更多请见[中文官方网站](https://iojs.org/cn/index.html)。

## 安装

进入官方网站，下载对应平台的安装包安装即可。

安装后在命令行执行如下命令显示 node 版本，确认安装无误。

```bash
$ node --version
```

## 版本管理

为了更方便的管理和更新 node.js 的版本，我们一般使用 nvm 工具。

安装 nvm 后，就可以安装、更新、指定使用哪个版本的 node。

```bash
$ curl https://raw.githubusercontent.com/creationix/nvm/v0.24.1/install.sh | bash
```

`ls` 命令用于查看本地所安装的版本。

```bash
$ nvm ls
```

`ls-remot` 命令用于查看服务器上所有可供安装的版本。

```bash
$ nvm ls-remote
```

`install` 命令用于安装指定版本的 node。

```bash
$ nvm install 0.11.12
```

其他用法等待你来发掘：

```bash
$ nvm -h
```

## 基本使用

例如运行当前目录下的 example.js 文件，可以这样写。

```bash
$ node ./example.js
```

## REPL 环境

直接在命令行执行 `node` 命令，进入 `REPL`（Read–eval–print loop，"读取-求值-输出"循环） 环境。

```bash
$ node
> 1 + 2
> 3
```
