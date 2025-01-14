---
title: ProcessBuilder和Process类API整理
categories: 
  - 编程
  - Java
  - Java 基础
  - API整理
date: 2019-09-30 22:59:36
updated: 2021-03-20 08:03:48
abbrlink: e5bb3a41
---
<div id='my_toc'><a href="/blog/e5bb3a41/#ProcessBuilder-API整理" class="header_1">ProcessBuilder API整理</a>&nbsp;<br><a href="/blog/e5bb3a41/#内部类" class="header_2">内部类</a>&nbsp;<br><a href="/blog/e5bb3a41/#构造器" class="header_2">构造器</a>&nbsp;<br><a href="/blog/e5bb3a41/#方法" class="header_2">方法</a>&nbsp;<br><a href="/blog/e5bb3a41/#取出或设置程序和参数的方法" class="header_3">取出或设置程序和参数的方法</a>&nbsp;<br><a href="/blog/e5bb3a41/#取出或设置工作目录的方法" class="header_3">取出或设置工作目录的方法</a>&nbsp;<br><a href="/blog/e5bb3a41/#设置标准IO的方法" class="header_3">设置标准IO的方法</a>&nbsp;<br><a href="/blog/e5bb3a41/#取出标准IO的方法" class="header_3">取出标准IO的方法</a>&nbsp;<br><a href="/blog/e5bb3a41/#合并标准输出相关的方法" class="header_3">合并标准输出相关的方法</a>&nbsp;<br><a href="/blog/e5bb3a41/#其他方法" class="header_3">其他方法</a>&nbsp;<br><a href="/blog/e5bb3a41/#启动进程方法" class="header_3">启动进程方法</a>&nbsp;<br><a href="/blog/e5bb3a41/#Process类API整理" class="header_1">Process类API整理</a>&nbsp;<br><a href="/blog/e5bb3a41/#杀死子进程" class="header_2">杀死子进程</a>&nbsp;<br><a href="/blog/e5bb3a41/#获取子进程的IO" class="header_2">获取子进程的IO</a>&nbsp;<br><a href="/blog/e5bb3a41/#其他方法" class="header_2">其他方法</a>&nbsp;<br><a href="/blog/e5bb3a41/#等待子进程" class="header_2">等待子进程</a>&nbsp;<br><a href="/blog/e5bb3a41/#实例" class="header_1">实例</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# ProcessBuilder API整理
## 内部类
|方法|描述|
|:---|:---|
|`static class ProcessBuilder.Redirect`|表示子进程的输入源或者输出的目的|

## 构造器
|方法|描述|
|:---|:---|
|`ProcessBuilder`​(`String... command)`|使用操作系统程序 和参数创建一个进程生成器|
|`ProcessBuilder`​(`List<String> command)`|使用操作系统程序和参数创建一个进程生成器|
## 方法

### 取出或设置程序和参数的方法
|方法|描述|
|:---|:---|
|`List<String> command()`|返回操作系统程序和该程序的参数。|
|`ProcessBuilder command(List<String> command)`|设置这个进程生成器的 操作系统程序 和 参数。|
|`ProcessBuilder command(String... command)`|置这个进程生成器的 操作系统程序 和 参数。|

### 取出或设置工作目录的方法
|方法|描述|
|:---|:---|
|`File directory()`|返回此进程生成器的工作目录。|
|`ProcessBuilder directory(File directory)`|设置进程生成器的工作目录。|

### 设置标准IO的方法
|方法|描述|
|:---|:---|
|`ProcessBuilder redirectOutput(File file)`|使用文件作为标准输出|
|`ProcessBuilder redirectOutput(ProcessBuilder.Redirect destination)`|使用`Redirect`对象作为标准输出|
|`ProcessBuilder redirectInput(File file)`|重定向标准输入到文件中|
|`ProcessBuilder redirectInput(ProcessBuilder.Redirect source)`|重定向标准输入|
|`ProcessBuilder redirectError(File file)`|将标出错误输出设置到文件中|
|`ProcessBuilder redirectError(ProcessBuilder.Redirect destination)`|设置标准错误输出的目标|

### 取出标准IO的方法
|方法|描述|
|:---|:---|
|`ProcessBuilder.Redirect redirectInput()`|返回表示`标准输入`的Redirect实例|
|`ProcessBuilder.Redirect redirectError()`|返回表示`标准错误输出`的Redirect实例|
|`ProcessBuilder.Redirect redirectOutput()`|返回表示`标出输出`的目标的Redirect实例|

### 合并标准输出相关的方法
|方法|描述|
|:---|:---|
|`ProcessBuilder inheritIO()`|子进程和父进程使用相同的标准输入,标准输出,标准错误输出|
|`ProcessBuilder redirectErrorStream(boolean redirectErrorStream)`|设置`redirectErrorStream`属性 |
|`boolean redirectErrorStream()`|判断进程生成器是否合并了标准错误输出和标准输出。|

### 其他方法
|方法|描述|
|:---|:---|
|`Map<String,String> environment()`|返回保存进程生成器的环境变量的`Map`集合|
### 启动进程方法
|方法|描述|
|:---|:---|
|`Process start()`|使用进程生成器中设置的属性启动新一个新的进程|

# Process类API整理

## 杀死子进程
|方法|描述|
|:---|:---|
|`abstract void destroy()`|杀死子流程|
|`Process destroyForcibly()`|杀死子流程|

## 获取子进程的IO
|方法|描述|
|:---|:---|
|`abstract InputStream getErrorStream()`|返回连接到子进程的错误输出的输入流|
|`abstract InputStream getInputStream()`|返回连接到子进程的正常输出的输入流.|
|`abstract OutputStream getOutputStream()`|返回连接到子进程的正常输入的输出流|

## 其他方法
|方法|描述|
|:---|:---|
|`abstract int exitValue()`|返回子进程的退出值|
|`boolean isAlive()`|测试子流程是否有效|

## 等待子进程
|方法|描述|
|:---|:---|
|`abstract int waitFor()`|使当前线程等待`Process`对象表示的进程终止|
|`boolean waitFor(long timeout, TimeUnit unit)`|使当前线程在必要时等待，直到此`Process`对象代表的子进程终止或经过指定的等待时间为止。|

# 实例
