---
title: BufferedInputStream读数组方法和FileInputStream读数组方法的区别：
categories: 
  - 编程
  - Java
  - Java IO流
  - 基础
date: 2018-08-22 14:32:39
updated: 2021-03-20 08:44:48
abbrlink: d4b540e
---
<div id='my_toc'><a href="/blog/d4b540e/#区别" class="header_1">区别</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 区别
- `BufferedInputStream`读数组方法，尽量读满整个数组，然后再返回，所以可能会多次读取，才返回。
- 而`FileInputStream`的读数组方法只会读取一次，读到多少就返回多少。读取一次，就返回一次。不管数组有没有读满。
