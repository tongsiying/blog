---
title: eclipse发布web项目到tomcat的webapps中
categories: 
  - 编程
  - IDE
  - eclipse
date: 2018-12-11 20:43:57
updated: 2021-03-20 10:32:56
abbrlink: 37dcd881
---
<div id='my_toc'><a href="/blog/37dcd881/#问题描述" class="header_1">问题描述</a>&nbsp;<br><a href="/blog/37dcd881/#缺点" class="header_2">缺点</a>&nbsp;<br><a href="/blog/37dcd881/#解决方案" class="header_2">解决方案</a>&nbsp;<br><a href="/blog/37dcd881/#eclipse中设置把Web项目发布到Tomcat-webapps中" class="header_2">eclipse中设置把Web项目发布到Tomcat webapps中</a>&nbsp;<br><a href="/blog/37dcd881/#参考链接" class="header_1">参考链接</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 问题描述
在Eclipse中，默认会把Web项目发布到Eclipse的工作空间下的：
```
\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps
```
这个目录中
## 缺点
关掉eclipse后无法访问Web项目。因为Tomcat只会到自己目录下的webapps目录中去寻找Web项目，发布在其他地方的项目Tomcat是找不到的。
## 解决方案
设置eclipse，把web项目发布到Tomcat安装目录下的webapps目录中。
## eclipse中设置把Web项目发布到Tomcat webapps中
先在Servers中展开Tomcat中运行的项目，把这些项目先`remove`掉：
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/change_webapps/remove.png)
然后在Tomcat服务器上，右键，点击`open`:
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/change_webapps/open.png)
如果`Server locations`是灰色的，这是因为Tomcat没有启动，先启动，然后再进行下面的操作,如果不是灰色则跳过这步：
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/change_webapps/gray.png)
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/change_webapps/start.png)
展开`Server locations`，可以看到这里默认选了第一个`Use workspace metadata(does not modify Tomcat installation`，这个表示发布到eclipse自己的目录中。**我们选择第二个**`Use Tomcat installation(takes control of Tomcat installation)`这个表示发布到Tomcat安装目录中。
然后在`deploy path:`中填入tomcat安装目录下的webapps目录,如下图所示：
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/change_webapps/settings.png)
最后，重启eclipse中的tomcat服务器，它会提示让你**保存**配置，点击保存保存我们上面的设置：
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/change_webapps/save.png)
然后在运行我们的项目，打开Tomcat安装目录下的webapps目录，可以在里面看到了我们的HelloWrold项目已经发布到这里了：
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/change_webapps/deploy_yes.png)
关闭eclipse，用命令直接打开Tomcat服务器，这个时候也是能访问我们的Web项目的：
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/change_webapps/startTomcat.png)
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/IDESetting/eclipse/change_webapps/helloworld.png)

# 参考链接
[https://www.cnblogs.com/mihu/p/4772509.html](https://www.cnblogs.com/mihu/p/4772509.html)
