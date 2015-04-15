NPM 篇
======

## 简介

npm 是 Node.js 的模块管理器，是一款命令行软件，用来安装和管理node模块。[官网](https://www.npmjs.com/)

npm 集成在 Node.js 安装包内，安装了 Node.js 就可以直接使用，不需要单独安装。

- 下载三方模块
- 上传自己的模块

## 安装模块

```bash
$ npm install [package name]
$ npm install -g [package name]
```

模块可以`本地安装`，也可以`全局安装`。主要差异是模块在系统的位置和安装位置和调用方法。

`全局安装` 是将模块直接安装到 Node.js 全局环境中。`本地安装`
是将模块下载到当前目录的 node_modules。

### 常用参数

安装命令可以使用不同参数，指定所安装的模块属于哪种依赖，主要体现在
`packages.json` 文件中。

```
--save：模块名将被添加到dependencies
--save-dev: 模块名将被添加到devDependencies
--save-optional：模块名将被添加到optionalDependencies
```

## 调用

```js
var p = require('p');
```

## 更新

```bash
$ npm update [package name]
```

## 卸载

```bash
$ npm uninstall [package name]
```

## 发布模块

```bash
$ npm publish [package name]
```

## 其他常用命令

```
$ npm help # 显示命令
$ npm -l   # 显示常规用法
$ npm config list -l # 显示当前配置
```

## 源
