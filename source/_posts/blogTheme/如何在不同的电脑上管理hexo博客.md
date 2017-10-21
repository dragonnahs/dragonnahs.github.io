---
title: 在不通过电脑上如何使用hexo搭建博客
date: 2017-07-30 21:20:06
tags: [hexo,blog,theme,next]
categories: 笔记
---

如何在不同电脑上管理自己的hexo个人博客，按照文章实现不同电脑管理自己hexo个人博客
<!-- more -->


# 如何在不同的电脑上管理hexo博客

## 前期准备

> [博客地址](https://dragonnahs.github.io/)


- 首先是要电脑上安装了git node
- 安装hexo

```

npm install hexo-cli -g

```
在项目目录下安装
```
npm install hexo --save

```
到这里是安装完了 hexo

```

hexo -v

```
通过上面的命令来检查是否安装成功，显示安装的hexo的版本。


## hexo 初始化

    
- 具体操作的流程如下：

```
hexo init 


```

```

npm install

```

```
hexo d
hexo s

```
清除并在本地运行，在本地访问localhost:4000访问页面。

## 部署到github page 


    
    

 


## 工作电脑




## 在另一台电脑上

直接clone

```
git clone url

```

之后进行安装相应的依赖包（忽略文件）

```
npm install hexo 
npm install 
npm install hexo-deployer-git --save

```
在本地访问

```
hexo d 
hexo s

```



写之后
```
git add .
git commit -m 'xx'
git push origin hexo // 保存原始代码
hexo d -g // 用于访问blog的操作，将页面部署

```

>  [参考链接](http://chown-jane-y.coding.me/2017/03/15/%E5%A6%82%E4%BD%95%E5%9C%A8%E4%B8%8D%E5%90%8C%E7%94%B5%E8%84%91%E4%B8%8A%E5%90%8C%E6%97%B6%E5%86%99hexo%E5%8D%9A%E5%AE%A2%EF%BC%9F/)


