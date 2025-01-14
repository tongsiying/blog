---
title: Ubuntu 安装intellij IDEA Ultimate
categories: 
  - 编程
  - Linux
  - VirtualBox
  - Ubuntu
date: 2019-11-25 17:52:23
updated: 2021-03-20 10:16:31
abbrlink: fa17fccd
---
<div id='my_toc'><a href="/blog/fa17fccd/#Ubuntu安装intellij-IDEA-Ultimate" class="header_1">Ubuntu安装intellij IDEA Ultimate</a>&nbsp;<br><a href="/blog/fa17fccd/#下载压缩包-tar-gz" class="header_2">下载压缩包(.tar.gz)</a>&nbsp;<br><a href="/blog/fa17fccd/#移动压缩包到要安装的路径" class="header_2">移动压缩包到要安装的路径</a>&nbsp;<br><a href="/blog/fa17fccd/#进入复制后的路径" class="header_2">进入复制后的路径</a>&nbsp;<br><a href="/blog/fa17fccd/#解压压缩包" class="header_2">解压压缩包</a>&nbsp;<br><a href="/blog/fa17fccd/#进入bin目录" class="header_2">进入bin目录</a>&nbsp;<br><a href="/blog/fa17fccd/#启动idea" class="header_2">启动idea</a>&nbsp;<br><a href="/blog/fa17fccd/#创建桌面快捷方式" class="header_2">创建桌面快捷方式</a>&nbsp;<br><a href="/blog/fa17fccd/#在桌面创建idea-desktop" class="header_3">在桌面创建idea.desktop</a>&nbsp;<br><a href="/blog/fa17fccd/#参考资料" class="header_1">参考资料</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# Ubuntu安装intellij IDEA Ultimate
## 下载压缩包(.tar.gz)
进入[Linux下载路径](https://www.jetbrains.com/idea/download/download-thanks.html?platform=linux)
## 移动压缩包到要安装的路径
例如,我这里从桌面复制到`/usr/java/`这个路径下:
```shell
sudo cp ~/桌面/ideaIU-2019.2.4.tar.gz /usr/java/
```
## 进入复制后的路径
```shell
cd /usr/java/
```
## 解压压缩包
```shell
sudo tar -zxvf /usr/java/ideaIU-2019.2.4.tar.gz
```
## 进入bin目录
```shell
cd idea-IU-192.7142.36/bin/
```
## 启动idea
```shell
./idea.sh
```
剩下的和Window上的操作一样
## 创建桌面快捷方式
每次进入`idea`安装路径下执行`idea.sh`还是挺麻烦的,下面介绍在桌面创建这个`idea.sh`的快捷方式.
### 在桌面创建idea.desktop
```shell
cd ~/桌面
touch idea.desktop
vim idea.desktop
```
然后`vim idea.desktop`,然后写入如下内容:
```shell
[Desktop Entry]
Name=IntelliJ IDEA
Type=Application
Comment=IntelliJ IDEA
Exec=/usr/java/idea-IU-192.7142.36/bin/idea.sh
Icon=/usr/java/idea-IU-192.7142.36/bin/idea.png
Terminal=false
Categories=Developer;
```
你只需要修改`Exec`和`Icon`这两个选项为你实际的路径即可.其他的不用管。这样点击就可以运行了,点击的时候会让你选择是否信任,点击`信任`即可

# 参考资料
[https://blog.csdn.net/qq_40950957/article/details/81386387](https://blog.csdn.net/qq_40950957/article/details/81386387)
