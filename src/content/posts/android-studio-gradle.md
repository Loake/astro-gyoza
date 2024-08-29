---
title: 如何解决Android Studio Gradle同步失败的问题
date: 2024-08-29T03:32:00.000Z
summary: 解决Gradle同步失败的问题
category: 教程
tags: [Android Studio, 教程]
---

> 本文中所用到的方法均为个人经验和来自于互联网的资料，如有错误，请指正。

# 前言

在Android Studio中，Gradle是一个重要的构建工具，用于编译和打包Android应用程序。有时候，Gradle可能会出现同步失败的情况，这可能是由于网络问题、Gradle版本不兼容或者配置错误等原因导致的。

Android Studio在创建一个项目后，会自动下载Gradle并自动同步，但是有时候会出现同步失败的情况。
如果你的gradle部署和同步失败，那么 `active_main.xml` 文件就无法正常显示，这会导致你的项目无法正常运行。
![gradle_build.png](https://s2.loli.net/2024/08/29/5MpcJYZrIFtNa7U.png '这是构建中，可以看到左下角同步信息哪里已经使用了13分钟')

![gradle_build_error.png](https://s2.loli.net/2024/08/29/2lwduUQj4fF39oS.png '构建同步失败，超时')

出现这种情况的原因是因为Android Studio默认从gradle官网下载Gradle，而官网的Gradle下载速度非常慢，导致下载失败，同步失败。

# 解决方法

这个问题困扰了很久，在网上搜集资料以后整理了一下解决方法

## 方法一：使用国内镜像源

国内有很多镜像源，比如阿里云、华为云、腾讯云等，都可以提供Gradle的镜像下载。

<del>[阿里云gradle镜像源](https://mirrors.aliyun.com/gradle)</del>

[华为云gradle镜像源](https://mirrors.huaweicloud.com/gradle)

[腾讯云gradle镜像源](https://mirrors.cloud.tencent.com/gradle)

[清华大学gradle镜像源](https://mirrors.tuna.tsinghua.edu.cn/gradle)

**_可惜的是，[阿里云gradle镜像源](https://mirrors.aliyun.com/gradle)源截至2019年就不再更新，gradle版本也停留在了gradle-5.6.2，若你使用的是gradle-5.6.2以上版本，更推荐你使用以上其他gradle镜像源_**

接下来找到你的项目文件夹内的 `gradle > wrapper > gradle-wrapper.properties` 文件

![gradle_build_file.png](https://s2.loli.net/2024/08/29/sdDoz4JaZi9u2WI.png '图中蓝色框内的即为下载gradle的url地址，但是它是官方的下载地址，速度很慢')

将 `distributionUrl=https\://services.gradle.org/distributions/gradle-8.7-bin.zip` 替换为 `distributionUrl=https\://mirrors.huaweicloud.com/gradle/gradle-8.7-bin.zip` ，例如：

```properties
distributionUrl=https\://mirrors.huaweicloud.com/gradle/gradle-7.5-bin.zip
```

更改完url地址后别忘了按`Ctrl + S` 保存文件，然后点击上面的 Try Again 重新同步项目即可。

但是这种方法在每次创建新的项目时都需要手动修改，所以不是很方便。于是就有了方法二

## 方法二：手动下载Gradle

在上面的链接手动下载Gradle对应的版本，然后将下载好的Gradle放到Android Studio的缓存目录中，然后在 `gradle-wrapper.properties` 文件中指定Gradle的路径。

如果你的配置是这样，那么他的绝对路径可能是 `C:\Users\你的用户名\.gradle\wrapper\dists` 这里存放了你的gradle下载的所有版本，你可以下载后解压到这个文件夹内

点击菜单栏的 `项目结构` -> `Gradle Vision` 确认你的项目的Gradle版本。在上面的链接手动下载Gradle对应的版本，然后将下载好的Gradle放到Android Studio的缓存目录中，然后在 `gradle-wrapper.properties` 文件中指定Gradle的路径。

随后：

1. 打开Android Studio，点击菜单栏的 `文件` -> `设置`。
2. 在设置窗口中，选择 `构建、执行、部署` -> `构建工具` -> `Gradle`。
3. 在分发那一栏点击下拉栏选择本地分发

![gradle_build_choose.png](https://s2.loli.net/2024/08/29/KEaz2kr8GfsZ1LB.png)

4. 点击浏览选择你刚刚解压的gradle文件夹，例如我的路径是 `C:\Users\你的用户名\.gradle\wrapper\dists\gradle-8.7-bin`

![gradle_build_path.png](https://s2.loli.net/2024/08/29/zhQqtYKE6TSWlBL.png)

5. 点击应用，然后点击确定

完成以上步骤后，你的Android Studio就配置好了Gradle的镜像源。然后点上面的Try Again 重新同步项目即可。

## 方法三：使用魔法

如果你可以 \*科\*学\*上\*网\* ，你可以在构建的时候直接使用ta来加速下载Gradle。
