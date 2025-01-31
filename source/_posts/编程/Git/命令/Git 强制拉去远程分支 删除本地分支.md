---
title: Git 强制拉去远程分支 删除本地分支
categories: 
  - 编程
  - Git
  - 命令
date: 2019-12-03 19:17:52
updated: 2020-04-11 09:21:19
abbrlink: ecbd02e2
---
<div id='my_toc'><a href="/blog/ecbd02e2/#问题描述" class="header_1">问题描述</a>&nbsp;<br><a href="/blog/ecbd02e2/#解决方案" class="header_1">解决方案</a>&nbsp;<br><a href="/blog/ecbd02e2/#方案1-删除本地仓库-重新克隆src分支" class="header_2">方案1 删除本地仓库 重新克隆src分支</a>&nbsp;<br><a href="/blog/ecbd02e2/#方案2-下载src分支-然后删除本地master分支" class="header_2">方案2 下载src分支 然后删除本地master分支</a>&nbsp;<br><a href="/blog/ecbd02e2/#删除远程master分支的记录" class="header_3">删除远程master分支的记录</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 问题描述
我的博客源码放在src分支上,pages放在master分支上,但是今天我在另一个电脑上想写博客,但是我克隆博客源码的时候输错了命令,不小心克隆到了master分支上.master分支上的pages是自动部署的,不需要我操作,我不想再本地上看到任何master分支的内容.
# 解决方案
## 方案1 删除本地仓库 重新克隆src分支
```shell
cd ..
rm -rf blogRoot/
git clone -b src git@github.com:lanlan2017/lanlan2017.github.io.git
```
## 方案2 下载src分支 然后删除本地master分支
```shell
git fetch origin src:src
git checkout src 
git branch -d master
```
### 删除远程master分支的记录
查看远程仓库地址:
```shell
 u0_a391@localhost ~/my/blogRoot> (src) git remote -v                                                                   
origin	git@github.com:lanlan2017/lanlan2017.github.io.git (fetch)
origin	git@github.com:lanlan2017/lanlan2017.github.io.git (push)
```
先删除远程地址,然后再添加远程地址:
```shell
git remote remove origin
git remote add -t src origin git@github.com:lanlan2017/lanlan2017.github.io.git
```
拉去远程src分支,这样本地上就只有远程上的src分支的记录:
```shell
 u0_a391@localhost ~/my/blogRoot> (src) git pull origin src 
From github.com:lanlan2017/lanlan2017.github.io
 * branch            src        -> FETCH_HEAD
 * [new branch]      src        -> origin/src

```
