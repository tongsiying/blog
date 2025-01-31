---
title: eclipse报错解决
categories: 
  - 编程
  - IDE
  - eclipse
date: 2020-06-23 12:38:43
updated: 2020-06-23 01:01:06
abbrlink: cec44542
---
<div id='my_toc'><a href="/blog/cec44542/#错误信息-Multiple-annotations-found-at-this-line" class="header_1">错误信息 Multiple annotations found at this line:</a>&nbsp;<br><a href="/blog/cec44542/#解决方案" class="header_2">解决方案</a>&nbsp;<br><a href="/blog/cec44542/#eclipse导出可执行jar时Launch-configuration下拉列表选项太多" class="header_1">eclipse导出可执行jar时Launch configuration下拉列表选项太多</a>&nbsp;<br><a href="/blog/cec44542/#解决方案" class="header_2">解决方案</a>&nbsp;<br><a href="/blog/cec44542/#参考资料" class="header_2">参考资料</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 错误信息 Multiple annotations found at this line:
springmvc配置文件报错如下:
![这里有一张图片](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/SpringMVCError/1.png)
```
Multiple annotations found at this line:
    - Referenced file contains errors (http://www.springframework.org/schema/context/spring-context.xsd). For more information, right click on the 
     message in the Problems View and select "Show Details..."
    - Referenced file contains errors (http://www.springframework.org/schema/mvc/spring-mvc.xsd). For more information, right click on the message 
     in the Problems View and select "Show Details..."
```
## 解决方案
依次打开:`Window>Preferences>XML>XML Files >Validation`
![这里有一张图片](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/SpringMVCError/2.png)
取消勾选:`Honour all XML schema locations`,它将禁用指向不同schema位置相同命名空间引用的验证，仅以第一次找到的可验证的XML文件为结果。 
然后点击`Apply and Close`
![这里有一张图片](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/SpringMVCError/3.png)
接下来选择`是`
![这里有一张图片](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/SpringMVCError/4.png)
这样就不会报错了，如下图所示:
![这里有一张图片](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/SpringMVCError/5.png)

# eclipse导出可执行jar时Launch configuration下拉列表选项太多
## 解决方案
如果想要删除`Launch configuration`下拉列表的主类历史记录，只要进入到要打包的这个`工程所在的目录`，也就是`工作空间目录`找到这个：
```
\.metadata\.plugins\org.eclipse.debug.core\.launches
```
文件夹，清空里面的内容，然后重启eclipse即可:
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDE%E4%BD%BF%E7%94%A8/eclipse%E5%AF%BC%E5%87%BA%E5%8F%AF%E6%89%A7%E8%A1%8Cjar%E6%97%B6Launch%20configuration%E9%80%89%E9%A1%B9%E5%A4%AA%E5%A4%9A/qingli_launch.png)
## 参考资料
[http://coderlxl201209164551.iteye.com/blog/2126652](http://coderlxl201209164551.iteye.com/blog/2126652)
