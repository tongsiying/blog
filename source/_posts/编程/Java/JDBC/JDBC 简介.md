---
title: JDBC 简介
categories: 
  - 编程
  - Java
  - JDBC
date: 2018-12-05 00:25:23
updated: 2021-03-20 09:24:39
abbrlink: aa45691f
---
<div id='my_toc'><a href="/blog/aa45691f/#JDBC-简介" class="header_1">JDBC 简介</a>&nbsp;<br><a href="/blog/aa45691f/#JDBC编程步骤" class="header_1">JDBC编程步骤</a>&nbsp;<br><a href="/blog/aa45691f/#加载驱动程序" class="header_2">加载驱动程序</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# JDBC 简介
JDBC全称为 `Java Data Base Connectivity` (java数据库连接)。JDBC是一种用于执行SQL语句的Java API，可以为多种关系数据库提供统一访问。
有了JDBC API，就不必为访问mysql数据库专门写一个程序，为访问Oracle数据库又专门写一个程序，或为访问sql server数据库又编写另一个程序等等，程序员只需用JDBC API写一个程序就够了。
# JDBC编程步骤
- 加载驱动程序 
- 获取数据库连接
- 创建Statemant对象

## 加载驱动程序
每个数据库都会提供JDBC的驱动开发包，直接把JDBC操作所需要的开发包(一般为.jar或.zip)添加到eclipse buildpath中即可。
