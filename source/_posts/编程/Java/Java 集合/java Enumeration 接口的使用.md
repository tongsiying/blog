---
title: java Enumeration 接口的使用
categories: 
  - 编程
  - Java
  - Java 集合
date: 2018-12-09 22:47:36
updated: 2021-03-20 09:26:30
abbrlink: 7b1e18da
---
<div id='my_toc'><a href="/blog/7b1e18da/#API中的介绍" class="header_1">API中的介绍</a>&nbsp;<br><a href="/blog/7b1e18da/#Enumeration接口方法" class="header_1">Enumeration接口方法</a>&nbsp;<br><a href="/blog/7b1e18da/#Enumeration接口遍历实例" class="header_1">Enumeration接口遍历实例</a>&nbsp;<br><a href="/blog/7b1e18da/#另一个遍历枚举的例子" class="header_1">另一个遍历枚举的例子</a>&nbsp;<br><a href="/blog/7b1e18da/#参考链接" class="header_1">参考链接</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->

# API中的介绍
> Enumeration（枚举）接口的功能与 Iterator 接口的功能是重复的。此外，Iterator 接口添加了一个可选的移除操作，并使用较短的方法名。新的实现应该优先考虑使用 Iterator 接口而不是 Enumeration 接口。 

# Enumeration接口方法
枚举接口只有以下两个方法：

|方法|描述|
|:-|:-|
|`boolean hasMoreElements()`|测试此枚举是否包含更多的元素。 |
|`E nextElement()`|如果此枚举对象至少还有一个可提供的元素，则返回此枚举的下一个元素。 |

虽然知道枚举已经过时了，但是在Java中有些地方还会用到Enumeration来进行输出,所以下面就来用一用这个接口
# Enumeration接口遍历实例
下面遍历输出JSP session内置对象中的所有的`属性/属性值`对，为什么举这个例子呢。因为，我看到`session.getAttributeNames();`这个方法的时候才了解有枚举这个东西。
```jsp
<%
session.setAttribute("user", "admin");
session.setAttribute("password", "123456");
//获取session中的所有属性的枚举
Enumeration<String> enu = session.getAttributeNames();
String attr = null;
//判断是否有属性
while (enu.hasMoreElements())
{
    //获取一个属性
    attr = enu.nextElement();
    //打印一个属性到控制台
    out.println("&nbsp;&nbsp;&nbsp;&nbsp;" + attr + "="
            + session.getAttribute(attr) + "<br>");
}
%>
```
# 另一个遍历枚举的例子
```java
public static void main(String[] args)
{
    Vector v = new Vector();
    v.addElement("Lisa");
    v.addElement("Billy");
    v.addElement("Mr Brown");
    Enumeration e = v.elements();//返回Enumeration对象
    while(e.hasMoreElements())
    {
        String value = (String)e.nextElement();//调用nextElement方法获得元素
        System.out.print(value);
    }
}
```
# 参考链接
[https://blog.csdn.net/qq924862077/article/details/48022185](https://blog.csdn.net/qq924862077/article/details/48022185)
