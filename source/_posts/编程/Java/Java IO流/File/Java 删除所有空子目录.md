---
title: Java 删除所有空子目录
categories: 
  - 编程
  - Java
  - Java IO流
  - File
date: 2018-12-22 19:15:36
updated: 2021-03-20 09:20:52
abbrlink: efd55c13
---
<div id='my_toc'><a href="/blog/efd55c13/#向下递归-删除所有空子目录" class="header_1">向下递归 删除所有空子目录</a>&nbsp;<br><a href="/blog/efd55c13/#向上递归-删除所有空父目录" class="header_1">向上递归 删除所有空父目录</a>&nbsp;<br><a href="/blog/efd55c13/#删除空目录完整代码" class="header_1">删除空目录完整代码</a>&nbsp;<br><a href="/blog/efd55c13/#测试" class="header_1">测试</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 向下递归 删除所有空子目录
删除方法如下所示：
```java
public static void deleteEmptyDIR(String dir)
{
    // 转成File对象
    File dirFile = new File(dir);
    // 获取列表
    File[] fileList = dirFile.listFiles();
    for (int i = 0; i < fileList.length; i++)
    {
        // 如果是目录的话
        if (fileList[i].isDirectory())
        {
            if (fileList[i].listFiles().length == 0)
            {
                if (fileList[i].delete())
                {
                    System.out.println("成功删除空目录:" + fileList[i].getAbsolutePath());
                }
            } else
            {
                // 递归下一个目录
                deleteEmptyDIR(fileList[i].getAbsolutePath());
            }
        }
    }
}
```
上述代码只能删除目录树中最末尾的空目录,有可能删除之后，又出现了空目录。但是此时递归已经结束了,新出现的空目录将无法删除。
1.这个时候可以先多运行几次，直到删除干净为止。
2.在上面的删除到目录树的最后的空子目录的时候，再递归向上删除空的父目录
# 向上递归 删除所有空父目录
```java
/**
 * 向上递归删除空目录
 * @param dir
 */
public static void deleteEmptyParentDIR(File dir)
{
    File parentFile = dir.getParentFile();
    // 如果dir目录的父目录为空的话
    if (parentFile.isDirectory() && parentFile.listFiles().length == 0)
    {
        if (parentFile.delete())
        {
            System.out.println("成功删除 父 目录>" + parentFile.getAbsolutePath());
            // 递归删除父目录
            deleteEmptyParentDIR(parentFile);
        }
    }
}
```
# 删除空目录完整代码
整合两者后代码如下：
```java
import java.io.File;
public class DeleteEmptyDir
{
    public static void main(String[] args)
    {
        // 获取目录
        String dirPath = "test";
        deleteEmptyDIR(dirPath);
    }
    /**
     * 向下递归,删除目录树中最后的空子目录.
     * @param dir
     */
    public static void deleteEmptyDIR(String dir)
    {
        // 转成File对象
        File dirFile = new File(dir);
        // 获取列表
        File[] fileList = dirFile.listFiles();
        for (int i = 0; i < fileList.length; i++)
        {
            // 如果是目录的话
            if (fileList[i].isDirectory())
            {
                // 如果当前是空目录
                if (fileList[i].listFiles().length == 0)
                {
                    // 删除当前的空目录
                    if (fileList[i].delete())
                    {
                        System.out.println("成功删除 空 目录>" + fileList[i].getAbsolutePath());
                        // 往回删除父目录
                        deleteEmptyParentDIR(fileList[i]);
                    }
                } else
                {
                    // 递归下一个目录
                    deleteEmptyDIR(fileList[i].getAbsolutePath());
                }
            }
        }
    }
    /**
     * 向上递归删除空目录
     * @param dir
     */
    public static void deleteEmptyParentDIR(File dir)
    {
        File parentFile = dir.getParentFile();
        // 如果dir目录的父目录为空的话
        if (parentFile.isDirectory() && parentFile.listFiles().length == 0)
        {
            //如果父目录删除成功
            if (parentFile.delete())
            {
                System.out.println("成功删除 空 父 目录>" + parentFile.getAbsolutePath());
                // 再递归删除父目录的父目录
                deleteEmptyParentDIR(parentFile);
            }
        }
    }
}
```
# 测试
测试目录结构如下：
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/Java%20IO/File/delete/emptyDirs/example.png)
运行结果：
```cmd
成功删除 空 目录>D:\dev\workspace\Test\test\test1\test2\test22
成功删除 空 目录>D:\dev\workspace\Test\test\test1\test2\test3\test4
成功删除 空 父 目录>D:\dev\workspace\Test\test\test1\test2\test3
成功删除 空 目录>D:\dev\workspace\Test\test\test1\test2\test33
成功删除 空 父 目录>D:\dev\workspace\Test\test\test1\test2
```
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/Java%20IO/File/delete/emptyDirs/delete.png)
