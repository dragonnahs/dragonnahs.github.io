---
title: vue项目的构建打包和发布
date: 2017-07-18 10:20:11
tags: [vue,坑,笔记]
categories: 笔记
---

vue项目的构建，打包，和发布，采用vue-cli进行初始化构建项目。
<!-- more -->

### vue构建，打包，发布

### 一、项目的构建

- 一般可以使用vue-cli进行项目构建，使用vue全家桶编写项目代码

```
// 基于webpack 模板进行构建
vue init webpack my-project
// 安装依赖
cd my-project
npm install
// 运行项目
npm run dev

```

### 二、项目的打包

- 使用 `npm run build ` 进行项目打包，生成dist文件，但是访问index.html文件使会报错，路径不正确，一般是要把config中的index.js文件中的 build->assetsPublicPath属性的值改为'./'


### 三、项目发布

- 把项目放到服务器。

[贴一个自己的小demo](https://github.com/dragonnahs/musicApp) 有兴趣的朋友可以看下

