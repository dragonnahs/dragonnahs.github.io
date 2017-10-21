---
title: gulp用法(1)
date: 2016-11-15 10:09:06
tags: [gulp,工具]
categories: 开发工具
---

在这里主要记录下如何使用gulp进行js和css的压缩合并，进行MD5命名，并引入进html页面中
<!-- more -->

## 压缩合并js，css文件

在这里主要记录下如何使用gulp进行js和css的压缩合并，进行MD5命名，并引入进html页面中

### 安装Gulp插件到本地项目

```
npm init 
// 生成一个 package.json，里面是一些常规的配置信息

npm install gulp gulp-concat gulp-uglify gulp-minify-css gulp-rev gulp-rev-collector --save-dev
//- 安装插件到项目目录内

```

完成上面两步后，会在我们的项目内生成一个package.json文件以及一个node_modules目录

###　创建配置文件 gulpfile.js

在项目根目录内创建一个 gulpfile.js 文件，内容就是上面几个插件的配置信息：

```

var gulp = require('gulp');
var concat = require('gulp-concat');                            //- 多个文件合并为一个；
var minifyCss = require('gulp-minify-css');                     //- 压缩CSS为一行；
var uglify = require('gulp-uglify');                     //- 压缩CSS为一行；
var rev = require('gulp-rev');                                  //- 对文件名加MD5后缀
var revCollector = require('gulp-rev-collector');               //- 路径替换

gulp.task('concat', function() {                                //- 创建一个名为 concat 的 task
    gulp.src(['assets/css/*.css'])    //- 需要处理的css文件，放到一个字符串数组里
        .pipe(concat('main.min.css'))                            //- 合并后的文件名
        .pipe(minifyCss())                                      //- 压缩处理成一行
        .pipe(rev())                                            //- 文件名加MD5后缀
        .pipe(gulp.dest('./css'))                               //- 输出文件本地
        .pipe(rev.manifest())                                   //- 生成一个rev-manifest.json
        .pipe(gulp.dest('./rev/css'));                              //- 将 rev-manifest.json 保存到 rev 目录内
});
gulp.task('concatJs', function() {                                //- 创建人物名称
    gulp.src(['assets/js/jquery-1.11.1.min.js','assets/js/*.js'])    //- 需要处理的js文件，放到一个字符串数组里
        .pipe(concat('main.min.js'))                            //- 合并后的文件名
        .pipe(uglify())                                      //- 压缩处理成一行
        .pipe(rev())                                            //- 文件名加MD5后缀
        .pipe(gulp.dest('./js'))                               //- 输出文件本地
        .pipe(rev.manifest())                                   //- 生成一个rev-manifest.json
        .pipe(gulp.dest('./rev/js'));                              //- 将 rev-manifest.json 保存到 rev 目录内
});

gulp.task('rev', function() {
    gulp.src(['./rev/**/*.json', './*.html'])   //- 读取 rev-manifest.json 文件以及需要进行css名替换的文件
        .pipe(revCollector())                                   //- 执行文件内css名的替换
        .pipe(gulp.dest('./'));                     //- 替换后的文件输出的目录
});

gulp.task('default', ['concat','concatJs', 'rev']);


```

运行gulp就可以

需要引入的压缩后的js和css 的页面必须像这样引入

```
<link rel="stylesheet" href="css/main.min.css">
<script src="js/main.min.js"></script>

```

然后运行后就可以达到预期的目的 （就是和配置文件中的自定的文件名相同）

运行后的代码：

```

  <link rel="stylesheet" href="assets/js/fullcalendar/fullcalendar.min.css">
<script src="js/main-defcf34772.min.js"></script>

```