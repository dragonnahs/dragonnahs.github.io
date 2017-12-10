---
title: vue-cli 项目实例构建
date: 2017-11-05 21:03:53
tags: [vue,vue项目实例,vue-cli,vue-router,vuex]
categories: 笔记
---

记录自己工作中搭建一个项目的过程，项目只给出了前期的搭建过程，配置好了主界面的路由，项目的实际功能并未实现。
![logo](/img/vue.jpg)
<!-- more -->


# vue-cli项目构建

> 用vue-cli构建的项目实例，主要是搭建一个项目，里面页面功能并未实现。



## 步骤

``` bash
# 安装依赖
npm install

# 运行项目，运行地址：localhost:8082，接口配置地址在config/index.js文件中
npm run dev

# 运行打包 
npm run build

# 打包输出日志
npm run build --report
```

## 技术栈

> vue vue-router vuex sass

## 项目进程

1. 建立项目架构
2. 搭建头部和尾部公共模块
> 公用模块在`components`文件夹中，主要的页面内容是在`views`中，尽量提取公共页面
3. 配置路由模块
> 路由模块入口在`router/index.js`中，基本的路由已经配置，里面有相应的解释，以及进行页面跳转是否需要登录验证的配置，
登录验证在前端进行判断，通过登录时的token进行判断，在`router.beforeEach()`中进行判断。
4. 建立vuex模块 
> 已经建立基本的vuex模块，入口是`vuex/store.js`，并对数据进行了模块化，后续尽量把根据功能进行模块化划分
5. 静态页面的配置
> 如果是img标签，图片尽量放在`assets`文件夹中，如果是`background-image`属性，图片尽量放在static中，因为webpack在解析时的方式不一样，有可能解析的不正确。
6. 现在项目的构建暂时告一段落，项目的基本架构已经完成，还有ui框架未引入，可以根据自己的情况考虑使用哪个ui框架，可自行参考。


## 遇到的问题及解决情况
1. 获取dom元素
> 使用ref获取dom元素，给元素设置`ref='name'`定义dom属性，然后通过`this.$refs.name`获取dom元素，进行操作，更详细的可以 [vue中使用ref]()

2. 导航栏的样式及跳转，涉及到vuex和watch的使用
> 由于涉及到登录权限的验证，使得登录跳转的验证和登录后的跳转出现了问题，需要一个定位的数字，进行跟踪处理，
在全局的`berforeEach`中进行了验证，后续需要在此使用vuex的数据进行提交处理，第二个工作日处理。到此项目的搭建可以告一段落，后续是页面和功能的填充。
3. 在项目构建过程中遇到了刷新导航的选中状态和路由的不统一
> 这里采用的是使用的`this.$router.history.current`获取当前路由的信息，包括传递的参数等，然后在`mounted`钩子函数中调用就可以了。
4. 在`router.js`中获取`vuex`中的数据
> 可以使用 ` const useAuto = router.app.$options.store.state.user.userAuto `来获取使用，

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
