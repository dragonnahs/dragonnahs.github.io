---
title: git的使用笔记
date: 2016-11-11 13:09:04
tags: [git,工具]
categories: 开发工具
---
记录日常使用git的一些心得笔记，持续更新中
<!-- more -->

## git 使用笔记

> 记录日常使用git的一些心得笔记，持续更新中


1. 在本地已经存在文件时，怎么新建分支，并且合并分支，把分支推送到远程仓库.

    - 新建并切换分支，然后可以在该分支上继续写自己的代码。
    ```
        git checkout -b home
    
    ```
    
    - 提交代码。
    ``` 
        git add .
        git commit -m 'modify something'
        
    ```
    
    - 切换到主分支，并进行合并分支。
    ```
        git checkout master
        git merger home 
    
    ```
    
    - 把修改后的内容推送到远程仓库，这里是推送到主分支，在远程仓库是看不到本地新建的分支的。
    ```
        git push origin master
    
    ```
    
    - 把本地的分支推送到远程仓库，此时就能在远程仓库看到新建的分支了。(应该是git内部机制就是这样的，默认不会把本地的分支推送到仓库，不然本地有太多的分支都推送上去就太冗余了。)
    ``` 
        git push -u origin home:home
    
    ```
    
    
2. 在本地更新远程仓库

    > 远程仓库和本地内容不一致时，从远程仓库把代码更新下来。
    
    - 
    
    ```
        git fetch origin master:temp
    
    ```
    在本地建一个临时分支，并把远程仓库的内容拷贝到临时分支。
    
    -  比较临时分支(远程仓库)和本地有什么区别。
    ```
        git diff temp
    
    ```
    
    - 合并本地分支和临时分支。
    ```
        git merge temp 
    
    ```
    
    - 删除临时分支
    ```
        git branch -d temp
    
    ```
    
3. 更新指定分支代码

    - 更新指定分支代码
    ```
        git clone -b xxx URL
    
    ```
4. 删除分支和跟新分支

    - 跟新分支内容

    ```
        git pull
    
    ```
    - 删除本地分支和删除远程分支
    ```
        git branch -D xxxx
        git push origin :xxxx
    
    ```
    

```
    <center> <iframe name="iframe_canvas" src="http://douban.fm/partner/baidu/doubanradio" scrolling="no" frameborder="0" width="400" height="200"></iframe> </center>
```
    