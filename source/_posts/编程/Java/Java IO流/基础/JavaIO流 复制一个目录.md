---
title: JavaIO流 复制一个目录
categories: 
  - 编程
  - Java
  - Java IO流
  - 基础
date: 2018-08-10 23:32:16
updated: 2021-03-20 08:44:48
abbrlink: bda55058
---
<div id='my_toc'><a href="/blog/bda55058/#实现文件复制" class="header_1">实现文件复制</a>&nbsp;<br><a href="/blog/bda55058/#复制目录的算法" class="header_1">复制目录的算法</a>&nbsp;<br><a href="/blog/bda55058/#复制目录的实现代码" class="header_2">复制目录的实现代码</a>&nbsp;<br><a href="/blog/bda55058/#完整代码如下：" class="header_1">完整代码如下：</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
实现把一个目录中的所有内容复制到一个目录中去

# 实现文件复制

因为一个目录下的文件可能是字符文件，也可能是二进制文件，所以使用字节流来进行复制,这样能复制所有类型的文件。
```java
/**
 * 复制一个文件
 * @param srcFile 源文件
 * @param destFile 目的文件
 * @throws IOException
 */
public static void copyFile(String srcFile, String destFile)
        throws IOException
{
    FileInputStream in = new FileInputStream(srcFile);
    FileOutputStream out = new FileOutputStream(destFile);
    // 2097152(Byte)=2048(KB)=2M
    byte[] buffer = new byte[2097152];
    int size = 0;
    //每次读取一个字节数组
    while ((size = in.read(buffer)) != -1)
    {
        //读到多少写入多少
        out.write(buffer, 0, size);
    }
    in.close();
    out.close();
}
```

上述方法可以复制一个文件，我们可以在这个方法的基础之上实现目录的复制。

# 复制目录的算法

- 遍历该目录列表，如果列表项是文件就调用上面的copyFile()方法复制该文件
- 如果是该列表项是一个目录的话，就递归调用自己，复制该子目录。

## 复制目录的实现代码
```java
/**
 * 使用递归复制目录,
 * @param FromDir 源目录的路径名称
 * @param ToDir 目的目录的路径名称
 * @throws IOException
 */
public static void copyDir(String FromDir, String ToDir) throws IOException
{
    // 创建目录的File对象
    File srcDir = new File(FromDir);
    // 判断源目录是不是一个目录
    if (!srcDir.isDirectory())
    {
        //如果不是目录那就不复制
        return;
    }
    //创建目的目录的File对象
    File destDir = new File(ToDir);
    // 如果目的目录不存在
    if (!destDir.exists())
    {
        // 创建目的目录
        destDir.mkdir();
    }
    
    // 获取源目录下的File对象列表,每一个对象代表一个目录或者文件
    File[] srcDirList = srcDir.listFiles();
    // 遍历源目录File对象列表
    for (int i = 0; i < srcDirList.length; i++)
    {
        // 如果是目录的话
        if (srcDirList[i].isDirectory())
        {
            // 递归调用复制该目录
            copyDir(FromDir + File.separator + srcDirList[i].getName(),
                    ToDir + File.separator + srcDirList[i].getName());
        }
        // 如果是文件的话
        if (srcDirList[i].isFile())
        {
            // 调用复制文件的方法
            copyFile(FromDir + File.separator + srcDirList[i].getName(),
                    ToDir + File.separator + srcDirList[i].getName());
        }

    }
}
```
main方法中调用：
```java
public static void main(String[] args) throws IOException
{
    copyDir("FromDir", "ToDir");//复制当前工程下的FromDir目录中的内容到ToDir目录中。
}
```

当前eclipse中的目录结构如下：
![](https://i.imgur.com/WWYtG31.png)

运行后的目录结构：

![](https://i.imgur.com/Amy5dyL.png)

可以看到整个目录复制成功了。

# 完整代码如下：

```java
package copy.file;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class CopyDir
{
    public static void main(String[] args) throws IOException
    {
        copyDir("FromDir", "ToDir");
    }
    /**
     * 使用递归复制目录,
     * 
     * @param FromDir
     *            源目录的路径名称
     * @param ToDir
     *            目的目录的路径名称
     * @throws IOException
     */
    public static void copyDir(String FromDir, String ToDir) throws IOException
    {
        // 创建目录的File对象
        File srcDir = new File(FromDir);
        // 判断源目录是不是一个目录
        if (!srcDir.isDirectory())
        {
            // 如果不是目录那就不复制
            return;
        }
        // 创建目的目录的File对象
        File destDir = new File(ToDir);
        // 如果目的目录不存在
        if (!destDir.exists())
        {
            // 创建目的目录
            destDir.mkdir();
        }

        // 获取源目录下的File对象列表,每一个对象代表一个目录或者文件
        File[] srcDirList = srcDir.listFiles();
        // 遍历源目录File对象列表
        for (int i = 0; i < srcDirList.length; i++)
        {
            // 如果是目录的话
            if (srcDirList[i].isDirectory())
            {
                // 递归调用复制该目录
                copyDir(FromDir + File.separator + srcDirList[i].getName(),
                        ToDir + File.separator + srcDirList[i].getName());
            }
            // 如果是文件的话
            if (srcDirList[i].isFile())
            {
                // 调用复制文件的方法
                copyFile(FromDir + File.separator + srcDirList[i].getName(),
                        ToDir + File.separator + srcDirList[i].getName());
            }

        }
    }
    /**
     * 复制一个文件
     * 
     * @param srcFile
     *            源文件
     * @param destFile
     *            目的文件
     * @throws IOException
     */
    public static void copyFile(String srcFile, String destFile)
            throws IOException
    {
        FileInputStream in = new FileInputStream(srcFile);
        FileOutputStream out = new FileOutputStream(destFile);
        // 2097152(Byte)=2048(KB)=2M
        byte[] buffer = new byte[2097152];
        int size = 0;
        // 每次读取一个字节数组
        while ((size = in.read(buffer)) != -1)
        {
            // 读到多少写入多少
            out.write(buffer, 0, size);
        }
        in.close();
        out.close();
    }

}
```
