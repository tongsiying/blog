---
title: Java 基本数据类型
categories: 
  - 编程
  - Java
  - Java 基础
  - 基础
date: 2019-01-14 20:49:01
updated: 2021-03-20 08:13:52
abbrlink: 4badee62
mathjax: true
---
<div id='my_toc'><a href="/blog/4badee62/#基本数据类型" class="header_1">基本数据类型</a>&nbsp;<br><a href="/blog/4badee62/#整型" class="header_1">整型</a>&nbsp;<br><a href="/blog/4badee62/#整型的数值范围" class="header_2">整型的数值范围</a>&nbsp;<br><a href="/blog/4badee62/#直接给出的整数值默认为int类型" class="header_2">直接给出的整数值默认为int类型</a>&nbsp;<br><a href="/blog/4badee62/#数值的表示方式" class="header_2">数值的表示方式</a>&nbsp;<br><a href="/blog/4badee62/#自动类型转换" class="header_1">自动类型转换</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 基本数据类型
$$
基本数据类型
\begin{cases}
整数类型
\begin{cases}
byte\quad &1个字节 \\
short\quad &2个字节 \\
int\quad &4个字节 \\
long\quad &8个字节
\end{cases} \\
浮点类型 \begin{cases}
float\quad &4个字节 \\
double\quad &8个字节
\end{cases} \\
字符类型 char \quad 2个字节 \\
布尔类型 boolean
\end{cases}
$$
**Java只包含这8种基本数据类型**,值得指出的是,字符串`String`不是基本数据类型,字符串是一个类,也就`是个引用数据类型`。
# 整型
## 整型的数值范围
整型的数值范围为:
 $$(-2^{\text{所占比特为位数}-1}=-2^{\text{所占字节数}\times 8-1})\sim (2^{\text{所占比特为位数}-1}-1=2^{\text{所占字节数}\times 8-1}-1)$$例如
- 一个byte类型整数在内存里占8位,可以表示的数值范围为:$(-2^{1\times 8 -1}=-2^7=128)\sim (2^{1\times 8 -1}-1=2^7-1=127)$
- 一个short类型整数在内存里`占16位`,可以表示的数值范围为:$-32768(-2^{15})\sim 32767(2^{15}-1)$
- 一个int类型整数在内存里`占32位`,可以表示的数值范围为:$-2147483648(-2^{31})\sim 2147483647(2^{31}-1)$
- 一个long类型整数在内存里`占64位`,表数范围是:$(2^{64})\sim (2^{64}-1)$

## 直接给出的整数值默认为int类型
int是最常用的整数类型,因此在通常情况下,**直接给出一个整数值默认就是int类型**。除此之外,有如下两种情形必须指出:
- 如果直接将一个较小的整数值(在byte或 short类型的表数范围内)赋给一个byte或 short变量,系统会自动把这个整数值当成byte或者shot类型来处理。也就是 `byte a=1`,这里的整数1会直接当成byte类型来处理，`short x=3`,这里的整数`3`也会直接当成short类型来处理。
- 如果使用一个巨大的整数值(超出了int类型的表数范围)时,Java`不会`自动把这个整数值当成long类型来处理。**如果希望系统把一个整数值当成long类型来处理,应在这个整数值后增加l或者`L`作为后缀**。通常推荐使用大写的`L`,因为英文小写`l`很容易跟数字`1`搞混。也就是`long a=2147483648;`这样写，$(2^31-1+1=2147483648)$虽然在Long的表示范围之内，但是编译器还是认为它是一个int类型，`2147483648`超出了int的表示范围。所以在编译时会报错，正确的写法为`long a=2147483648L;`

可以把一个较小的整数值(在int类型的表数范围以内)直接赋给一个long类型的变量,这并不是因为Java会把这个较小的整数值当成long类型来处理,Java依然把这个整数值当成int类型来处理,只是因为**int类型的值会自动类型转换到long类型**。
## 数值的表示方式
Java中整数值有4种表示方式:十进制、二进制、八进制和十六进制,其中**二进制的整数以0b或0B开头**;**八进制的整数以0开头**;**十六进制的整数以0x或者0X开头**,其中10-15分别以a-f(此处的af不区分大小写)来表示。下面的代码片段分别使用八进制和十六进制的数。

# 自动类型转换
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/ShuJuLeiXing/1.png)
