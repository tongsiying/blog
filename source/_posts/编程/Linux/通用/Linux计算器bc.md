---
title: Linux计算器bc
categories: 
  - 编程
  - Linux
  - 通用
abbrlink: a04d41de
date: 2021-04-20 21:47:55
updated: 2021-04-20 23:07:47
---
<div id='my_toc'><a href="/blog/a04d41de/#Linux计算器bc" class="header_1">Linux计算器bc</a>&nbsp;<br><a href="/blog/a04d41de/#精度" class="header_2">精度</a>&nbsp;<br><a href="/blog/a04d41de/#命令设置缺省精度" class="header_3">命令设置缺省精度</a>&nbsp;<br><a href="/blog/a04d41de/#整数计算" class="header_4">整数计算</a>&nbsp;<br><a href="/blog/a04d41de/#小数计算" class="header_4">小数计算</a>&nbsp;<br><a href="/blog/a04d41de/#可以通过设置scale自行决定精度（小数点位数）" class="header_3">可以通过设置scale自行决定精度（小数点位数）</a>&nbsp;<br><a href="/blog/a04d41de/#设置bc计算器精确到小数点后10000位" class="header_4">设置bc计算器精确到小数点后10000位</a>&nbsp;<br><a href="/blog/a04d41de/#设置bc计算器精确到小数点后30位" class="header_4">设置bc计算器精确到小数点后30位</a>&nbsp;<br><a href="/blog/a04d41de/#bc编程" class="header_2">bc编程</a>&nbsp;<br><a href="/blog/a04d41de/#使用变量" class="header_3">使用变量</a>&nbsp;<br><a href="/blog/a04d41de/#查看变量" class="header_4">查看变量</a>&nbsp;<br><a href="/blog/a04d41de/#使用变量进行计算" class="header_4">使用变量进行计算</a>&nbsp;<br><a href="/blog/a04d41de/#使用循环" class="header_3">使用循环</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# Linux计算器bc
功能强大
- 基本计算器功能
- 支持变量、函数，条件和循环 等编程 功能（类似 C 语言的小编程语言）
- 可以进行任意精度的 计算

## 精度
### 命令设置缺省精度

|打开计算器的命令|描述|
|:---|:---|
|bc|缺省精度为小数点后 0 位|
|bc l|缺省精度 为小数点后 20 位|

#### 整数计算
```
[root@localhost ~]# bc
bc 1.06.95
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
1+2*3/4
2

```
#### 小数计算
```
[root@localhost ~]# bc -l
bc 1.06.95
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
1+2*3/4
2.50000000000000000000

```

### 可以通过设置scale自行决定精度（小数点位数）
#### 设置bc计算器精确到小数点后10000位
```
scale=10000
```
计算效果：
```
[root@localhost ~]# bc
bc 1.06.95
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
1+2*3/4
2
scale=10000
1+2*3/4
2.500000000000000000000000000000000000000000000000000000000000000000\
00000000000000000000000000000000000000000000000000000000000000000000\
00000000000000000000000000000000000000000000000000000000000000000000\
00000000000000000000000000000000000000000000000000000000000000000000\
00000000000000000000000000000000000000000000000000000000000000000000\
00000000000000000000000000000000000000000000000000000000000000000000\
00000000000000000000000000000000000000000000000000000000000000000000\
00000000000000000000000000000000000000000000000000000000000000000000\
00000000000000000000000000000000000000000000000000000000000000000000\
```
#### 设置bc计算器精确到小数点后30位
```shell
scale=30 #输入
1+2*3/4  #输入
2.500000000000000000000000000000 #计算结果

```
## bc编程
### 使用变量
#### 查看变量
在bc中输入变量的值，然后在输入变量名即可查看该变量的值：
```
p=20
p
```
运行效果
```
p=20
p
20
```
#### 使用变量进行计算
```
[root@localhost ~]# bc
bc 1.06.95
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
p=20    #输入
(2+p)*p #输入
440     #计算结果

```
### 使用循环
求1~128的阶乘，在bc中分别输入如下三行代码：
```c
s=1;          
for(i=1;i<128;i++) s*=i;
s
```
计算结果：
```
[root@localhost ~]# bc
bc 1.06.95
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
s=1;                     #输入
for(i=1;i<128;i++) s*=i; #输入
s                        #输入
30126600184576595448099770775270596923241649186736217990533469005966\
67207618480809067860692097713761984609779945772783965563851033300772\
32629777308785186998250027066179124412259762176000000000000000000000\
0000000000

```
