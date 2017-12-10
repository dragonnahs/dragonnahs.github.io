---
title: vue的博客项目后台用nodejs实现
date: 2017-11-08 22:46:23
tags: [vue,vue-cli,vue-router,node,mongodb]
categories: 笔记
---

一直想做一个前后台结合的项目，结合自己的情况写了一个简单的博客和后台管理系统，水平有限大家抱着批评的态度看看，不对的地方欢迎批评指正。

<!-- more -->


# vue实现博客功能和后台管理

> 前端是用vue-cli实现构建，后端是用的node express mongoose实现的，该项目需要安装mongodb，相关知识大家自行搜索哈。


## 前端开始步骤

``` bash
# 安装依赖
npm install

# 在本地运行 localhost:8089
npm run dev

# 运行打包
npm run build

```

# 后台使用node写的
[后台项目地址](https://github.com/dragonnahs/vue_blog_back)





## 后端开始步骤

> 这个项目是使用了nodejs链接的mongodb 需要安装mongodb并启动
安装mongodb可参考[安装mongodb](http://www.runoob.com/mongodb/mongodb-window-install.html)

```
# 安装依赖
npm install 

# 运行服务器
node server.js

# 启动mongodb

```
### 前端项目地址

[前端项目地址](https://github.com/dragonnahs/vue_blog_font)