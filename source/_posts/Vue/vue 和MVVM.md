---
title: vue 和 MVVM
date: 2017-06-20 11:22:01
tags: [MVVM,vue,]
categories: 笔记
---

记录下自己在学习vue中的一些理解，涉及到MVVM思想上的一些总结记录。
<!-- more -->


## 记录MVVM的一些认识

### 1、vue中的一些关于dom操作的繁琐思想

> vue 作者提出一般vue实现了频繁操作dom的缺点

在复杂的项目中，我们需要根据加载的数据，对dom元素进行频繁的操作，大量调用dom的api
，操作比较负责，代码冗余，维护起来比较麻烦，并且还会导致页面渲染缓慢，加载速度变慢，mvc模式中，只要model（管理数据层）层发生变化，我们就要主动更新view层，view层操作导致数据变化，也要更新到model层中，导致代码维护难度变大。这些促进MVVM模式的出现。

### 2、vue中的MVVM思想，双向数据绑定
vue和model没有直接的联系，viewModel把view和model联系起来，view的操作实时改变model，model数据的改变立即反应到view上，通过双向数据绑定将view和model联系到一起。
vue 采用Object.defineProperty的getter和setter，并结合观察者模式实现数据绑定,
普通对象传给vue实例时，vue会遍历这个对象的属性，并转化为getter和setter。通过vue追踪依赖，在属性被改变时通知发生变化。

### 3、Vue中的三个层面

- model 业务相关的数据对象（vue初始化中data对象）
- view 展现出来的用户界面（html代码）
- viewModel vue文件中的js部分，viewModel 是view和model的连接器，view和model通过viewModel实现双向数据绑定。
> viewModel 就相当于把model对象封装成可以显示和接收数据的界面数据对象