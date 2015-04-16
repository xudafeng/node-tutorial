## 介绍

Node.js 是 JavaScript
在服务器端的一个运行环境。它的JavaScript解释器，采用了Google 公司的 V8 引擎。

## io.js

io.js 是一个衍生自 Node.js™，并兼容 npm 的开发平台，更完美地支持 ES6。

## 安装

直接进入官方网站[nodejs.org](http://nodejs.org)，下载安装包即可。

```bash
$ node --version
```

安装成功之后可以通过如上命令查看版本。

## 版本管理

上面这条命令，安装最新的v0.10.x版本的node.js。

安装后，就可以指定使用该版本。

```bash
$ nvm use 0.11
```

ls命令用于查看本地所安装的版本。

```bash
$ nvm ls
```
ls-remote命令用于查看服务器上所有可供安装的版本。

```bash
$ nvm ls-remote
```

## 基本使用

例如运行当前目录下的 example.js 文件，可以这样写。

```bash
$ node ./example.js
```

## REPL 环境

直接在命令行执行 node命令，进入REPL环境（Read–eval–print loop，"读取-求值-输出"循环）。

```bash
$ node
> 1 + 2
> 3
```
