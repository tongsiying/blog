---
title: GCC编译C语言详解
categories: 
  - 编程
  - Linux
  - C语言
abbrlink: 58d9ef0d
date: 2021-04-03 22:15:32
updated: 2021-04-03 23:14:48
---
<div id='my_toc'><a href="/blog/58d9ef0d/#GCC简介" class="header_1">GCC简介</a>&nbsp;<br><a href="/blog/58d9ef0d/#演示代码" class="header_1">演示代码</a>&nbsp;<br><a href="/blog/58d9ef0d/#生成可执行程序" class="header_1">生成可执行程序</a>&nbsp;<br><a href="/blog/58d9ef0d/#gcc-源文件" class="header_2">gcc 源文件</a>&nbsp;<br><a href="/blog/58d9ef0d/#Linux不以后缀来区分可执行文件" class="header_3">Linux不以后缀来区分可执行文件</a>&nbsp;<br><a href="/blog/58d9ef0d/#gcc-源文件-o-可执行文件" class="header_2">gcc 源文件 -o 可执行文件</a>&nbsp;<br><a href="/blog/58d9ef0d/#在当前目录下输出可执行文件" class="header_3">在当前目录下输出可执行文件</a>&nbsp;<br><a href="/blog/58d9ef0d/#输出可执行文件到其他目录" class="header_3">输出可执行文件到其他目录</a>&nbsp;<br><a href="/blog/58d9ef0d/#运行可执行程序" class="header_1">运行可执行程序</a>&nbsp;<br><a href="/blog/58d9ef0d/#执行当前目录下的可执行程序" class="header_2">执行当前目录下的可执行程序</a>&nbsp;<br><a href="/blog/58d9ef0d/#执行其他目录下的可执行程序" class="header_2">执行其他目录下的可执行程序</a>&nbsp;<br><a href="/blog/58d9ef0d/#添加可执行全选" class="header_2">添加可执行全选</a>&nbsp;<br><a href="/blog/58d9ef0d/#参考资料" class="header_1">参考资料</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# GCC简介
GCC 仅仅是一个编译器，没有界面，必须在命令行模式下使用。通过gcc命令就可以将源文件编译成可执行文件。

GCC 既可以一次性完成C语言源文件的编译，也可以分步骤完成。本节将完整演示如何一次性完成源文件的编译（初学者也经常会这么做），下节将演示分步骤编译源文件。

# 演示代码
本节以下面的C语言代码为例进行演示：
```c
#include <stdio.h>
int main()
{
    puts("C语言中文网");
    return 0;
}
```
# 生成可执行程序
## gcc 源文件
最简单的生成可执行文件的写法为：在 gcc 命令后面紧跟源文件名，例如：
```
gcc main.c
```
接下来可以在当前目录中看到多了一个名为a.out的文件，这就是最终生成的可执行文件。
这样就一次性完成了编译和链接的全部过程，非常方便。
### Linux不以后缀来区分可执行文件
注意：不像 Windows，Linux 不以文件后缀来区分可执行文件，Linux 下的可执行文件后缀理论上可以是任意的，这里的.out只是用来表明它是 GCC 的输出文件。不管源文件的名字是什么，GCC 生成的可执行文件的默认名字始终是a.out。
## gcc 源文件 -o 可执行文件
### 在当前目录下输出可执行文件
如果不想使用默认的文件名，那么可以通过-o选项来自定义文件名，例如：
```
gcc main.c -o main.out
```
这样生成的可执行程序的名字就是main.out。

因为 Linux 下可执行文件的后缀仅仅是一种形式上的，所以可执行文件也可以不带后缀，例如：
```
gcc main.c -o main
```
这样生成的可执行程序的名字就是main。
### 输出可执行文件到其他目录
通过-o选项也可以将可执行文件输出到其他目录，并不一定非得在当前目录下，例如：
```
mkdir out
gcc main.c -o out/main.out
```
表示将可执行文件输出到当前目录下的out目录，并命名为main.out。./表示当前目录，如果不写，默认也是当前目录。
注意：out 目录必须存在，如果不存在，gcc 命令不会自动创建，而是抛出一个错误。

# 运行可执行程序
## 执行当前目录下的可执行程序
上面我们生成了可执行程序，那么该如何运行它呢？很简单，在控制台中输入程序的名字就可以，如下所示：
```
./a.out
```
./表示当前目录，整条命令的意思是运行当前目录下的 a.out 程序。如果不写./，Linux 会到系统路径下查找 a.out，而系统路径下显然不存在这个程序，所以会运行失败。
## 执行其他目录下的可执行程序
如果程序在其它目录下，运行程序时还要带上目录的名字，例如：
```
./out/main.out
```
或者
```
out/main.out
```
这个时候加不加./都一样，Linux 能够识别出out是一个目录，而不是一个命令，它默认会在当前路径下查找该目录，而不是去系统路径下查找，所以不加./也不会出错。
## 添加可执行全选
注意，如果程序没有执行权限，可以使用chmod命令来增加权限，例如：
```
sudo chmod 777 a.out
```
# 参考资料
GCC编译C语言程序完整演示：[http://c.biancheng.net/view/660.html](http://c.biancheng.net/view/660.html)
