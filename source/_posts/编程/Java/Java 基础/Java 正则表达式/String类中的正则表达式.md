---
title: String类中的正则表达式
categories: 
  - 编程
  - Java
  - Java 基础
  - Java 正则表达式
date: 2018-08-06 23:46:40
updated: 2021-03-20 07:44:48
abbrlink: 12fb64fe
---
<div id='my_toc'><a href="/blog/12fb64fe/#本文内容已丢失" class="header_1">本文内容已丢失</a>&nbsp;<br><a href="/blog/12fb64fe/#replaceFirst-方法" class="header_2">replaceFirst()方法</a>&nbsp;<br><a href="/blog/12fb64fe/#实例" class="header_3">实例</a>&nbsp;<br><a href="/blog/12fb64fe/#replaceAll-方法" class="header_2">replaceAll()方法</a>&nbsp;<br><a href="/blog/12fb64fe/#实例" class="header_3">实例</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 本文内容已丢失

所以平常使用的时候为了不分割到空字符串，还是设置`limit=0`比较好，可以就是直接调用`String.split(regex)`就行了。

## replaceFirst()方法
>String replaceFirst(String regex, String replacement) 
&emsp;&emsp;&emsp;&emsp;使用给定的 replacement 替换此字符串匹配给定的正则表达式的第一个子字符串。 调用此方法的 str.replaceFirst(regex, repl) 形式与以下表达式产生的结果完全相同： 
&emsp;&emsp;&emsp;&emsp;`Pattern.compile(regex).matcher(str).replaceFirst(repl)`

源码如下：
```java
public String replaceFirst(String regex, String replacement) 
{
    return Pattern.compile(regex).matcher(this).replaceFirst(replacement);
}
```
这个方法简直人如其名，我不知道该怎么详细些了。
### 实例
```java
String text="aaa:hahaha...";
System.out.println(text.replaceFirst("aaa", "I am groot"));
```
运行结果：
```
I am groot:hahaha...
```
##  replaceAll()方法
>`public String replaceAll(String regex,String replacement)`
>使用给定的 `replacement` 替换此字符串所有匹配给定的正则表达式的子字符串。 
调用此方法的 `str.replaceAll(regex, repl)` 形式与以下表达式产生的结果完全相同： &emsp;&emsp;&emsp;&emsp;`Pattern.compile(regex).matcher(str).replaceAll(repl)`

源码：
```java
public String replaceAll(String regex, String replacement) 
{
    return Pattern.compile(regex).matcher(this).replaceAll(replacement);
}

```
### 实例

```java
    String text="A:你好\nGtoot:_\nA:额，听不懂\nGroot:_\nA:。。。";
    text=text.replaceAll("A", "Tony Stark");
    System.out.println(text.replaceAll("_", "I am groot"));
```
运行结果：
```
Tony Stark:你好
Gtoot:I am groot
Tony Stark:额，听不懂
Groot:I am groot
Tony Stark:。。。

```
