---
title: vue-mongodb-node的使用笔记
date: 2017-06-11 19:09:04
tags: [node,vue,mongodb]
categories: 学习
---

前些天一直在重新学习vue2.0,网上的内容残次不齐，多番折腾也慢慢琢磨出些东西，后续会把学习的过程写出来，作为总结，有需要的朋友可以参考下
<!-- more -->


> 前些天一直在重新学习vue2.0,网上的内容残次不齐，多番折腾也慢慢琢磨出些东西，后续会把学习的过程写出来，作为总结，有需要的朋友可以参考下。

## 将node vue mongodb 链接起来

1. 首先已经安装过mongodb，建立起vue 模板，在根目录下创建server目录

- db.js存放mongodb代码

```
// 加载所需要的模块
const mongoose = require('mongoose')
mongoose.Promise = require('bluebird')
const Schema = mongoose.Schema

const UserSchema = new mongoose.Schema({
    username: String,//用户名
    sex: String,// 性别
    age: Number, // 年龄
},{collection:'user'}) 
// 注意这里一定要带有collection，否则mongoose会在下面model时对user添加后缀s.

const Models = {
    Login: mongoose.model('user', UserSchema)
}

/**
 * 创建数据库名称并连接
 * Connecting to Mongod instance.
 */
const dbHost = 'mongodb://localhost/testDb'
mongoose.connect(dbHost)
const db = mongoose.connection
db.on('error', function () {
    console.log('Database connection error.')
})
db.once('open', function () {
    console.log('The Database has connected.')
})

module.exports = Models

```
- api.js请求数据

```
// 可能是我的node版本问题，不用严格模式使用ES6语法会报错
"use strict"
const models = require('./db')
const express = require('express')
const router = express.Router()

/************** 创建(create) 读取(get) 更新(update) 删除(delete) **************/

// 创建账号接口
router.post('/api/login/createAccount',(req,res) => {
    // 这里的req.body能够使用就在index.js中引入了const bodyParser = require('body-parser')
    let newAccount = new models.Login({
        account : req.body.account,
        password : req.body.password
    });
    // 保存数据newAccount数据进mongoDB
    newAccount.save((err,data) => {
        if (err) {
            res.send(err)
        } else {
            res.send('createAccount successed')
        }
    });
});
// 获取已有账号接口
router.get('/api/login/getAccount',(req,res) => {
    console.log(222)
    // 通过模型去查找数据库
    models.Login.find((err,data) => {
        if (err) {
            res.send(err)
        } else {
            res.send(data)
        }
    })
})

    

module.exports = router

```
- index.js入口文件

```
// 引入编写好的api
const api = require('./api')
// 引入文件模块
const fs = require('fs')
// 引入处理路径的模块
const path = require('path')
// 引入处理post数据的模块
const bodyParser = require('body-parser')
// 引入Express
const express = require('express')
const app = express()

app.use(bodyParser.json())
app.use(bodyParser.urlencoded({extended: false}))
app.use(api);
// 访问静态资源文件 这里是访问所有dist目录下的静态资源文件
app.use(express.static(path.resolve(__dirname, '../dist')))
// 因为是单页应用 所有请求都走/dist/index.html
app.get('*', function(req, res) {
    const html = fs.readFileSync(path.resolve(__dirname, '../dist/index.html'), 'utf-8')
    res.send(html)
})
// 监听8088端口
app.listen(8088)
console.log('success listen…………')

```

> 然后直接在server目录下启动==node index== 运行代码，访问数据，访问++http://localhost:8088/api/login/getAccount++

- 解决前端访问数据时的跨域问题(在根目录下的config目录下的index.js找到proxyTable,改成下面的代码)

```
 proxyTable: {
      '/api': {
        target: 'http://localhost:8088/api/',
        changeOrigin: true,
        pathRewrite: {
          '^/api': ''
        }
      }

```


自己写了一个后台系统，附上链接地址 [后台管理系统](https://github.com/dragonnahs/login_work)