---
title: 免费手机投屏电脑神器 - scrcpy
summary: scrcpy是一个开源的 Android 设备屏幕远程控制工具，可以在电脑上显示和控制 Android 设备的屏幕。它支持通过 USB 连接或通过 Wi-Fi 连接进行远程控制。
date: 2024-07-27T19:42:48.504Z
tags: [投屏, scrcpy]
comments: true
draft: false
---

> 本文均根据[scrcpy官方仓库](https://github.com/Genymobile/scrcpy)进行整理，翻译与撰写，如有错误，请指正。<br>
> 因篇幅限制，本文仅提供Windows操作系统的操作方法，其他系统请移步[scrcpy官方中文文档](https://github.com/Genymobile/scrcpy/wiki/README.zh-Hans)查阅详情。多有不便，深感歉意！

# 目录

点击快速跳转

- [目录](#目录)
  - [前言](#前言)
  - [scrcpy 简介](#scrcpy-简介)
  - [先决条件](#先决条件)
  - [下载](#下载)
  - [安装](#安装)
  - [运行](#运行)
    - [USB投屏](#usb投屏)
    - [WiFi投屏](#wifi投屏)
  - [特殊情况](#特殊情况)
  - [FAQ](#faq)
    - [常见问题疑难解答](#常见问题疑难解答)
    - [adb相关问题](#adb相关问题)
      - [找不到adb](#找不到adb)
      - [设备未授权](#设备未授权)
      - [未检测到设备](#未检测到设备)
      - [已连接多个设备](#已连接多个设备)
      - [adb版本之间冲突](#adb版本之间冲突)
      - [设备断开连接](#设备断开连接)
    - [控制相关问题](#控制相关问题)
      - [鼠标和键盘不起作用](#鼠标和键盘不起作用)
      - [特殊字符不起作用](#特殊字符不起作用)
    - [客户端相关问题](#客户端相关问题)
      - [效果很差](#效果很差)
      - [Wayland相关的问题](#wayland相关的问题)
      - [KWin compositor 崩溃](#kwin-compositor-崩溃)
    - [崩溃](#崩溃)
      - [异常](#异常)
    - [Windows命令行](#windows命令行)
  - [参考](#参考)

## 前言

大家平时有没有遇到过需要将手机屏幕投放到电脑上，然后进行操作的情况呢？比如，在电脑上查看手机上的照片、视频，或者将手机上的内容投放到电脑上，以便在电脑上进行编辑、分享等操作。那么目前大多数控制软件只支持手机远程控制电脑，而电脑无法投屏或控制手机。

今天就给大家推荐一款免费、开源的 Android 设备屏幕远程控制工具 - scrcpy。

## scrcpy 简介

scrcpy 是一个开源的 Android 设备屏幕远程控制工具，可以在电脑上显示和控制 Android 设备的屏幕。
可以镜像通过USB或TCP/IP连接的Android设备(视频和音频)，并允许使用计算机的键盘和鼠标控制设备。它不需要任何根访问权限。它在Linux，Windows和macOS上工作。

scrcpy 的特点如下：

1. 开源：scrcpy 是一个开源项目，可以在 GitHub 上找到源代码，并且可以自由地修改和分发。
2. 免费使用：scrcpy 是免费的，不需要购买许可证或订阅服务。
3. 跨平台：scrcpy 支持在 Windows、macOS 和 Linux 上运行。
4. 高性能：scrcpy 可以以 60fps 的帧率显示 Android 设备的屏幕，并且可以在电脑上实时控制设备。

它侧重于：

- **轻量**：原生，仅显示设备屏幕
- **性能**：30~120fps（这取决于你设备的屏幕是否支持高帧率）
- **质量**：1920×1080及以上
- **低延迟**：35~70ms
- **快速启动**：最快 1 秒内即可显示第一帧
- **无侵入性**：Android设备上无需安装任何软件
- **用户利益**：不需要登录，没有广告，不需要联网（使用USB连接）
- **免费**：scrcpy是开源软件，免费使用

其特点包括：

- 音频转发（需要Android 11+）
- 屏幕录制
- 镜像时关闭 Android 设备的屏幕
- 双向复制粘贴
- 可配置显示质量
- 支持投屏时使用摄像头（需要Android 12+）
- 以 Android 设备作为摄像头 (V4L2)（仅限 Linux）
- 模拟物理键盘和物理鼠标模拟（HID）
- OTG模式
- 更多...

## 先决条件

**Android设备至少需要API 21（Android 5.0）**
确保你的设备启动了USB调试
在某些设备上，你还需要启用额外的选项`USB调试（安全设置）`（这是一个与USB调试不同的项目），以便使用键盘和鼠标进行控制。

## 下载

- [Windows](#安装)
- [官方网站](https://scrcpy.net/download/)

## 安装

去scrcpy的官方github仓库下载[最新版本](https://github.com/Genymobile/scrcpy/releases/)：

- [scrcpy-win64bit-v2.5.zip (64位)](https://objects.githubusercontent.com/github-production-release-asset-2e65be/111583593/a82a7d5d-910b-4037-ae90-5fc88c6b77f1?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=releaseassetproduction%2F20240727%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240727T171401Z&X-Amz-Expires=300&X-Amz-Signature=0cd36dbc80c5a330e80693ebd1924f48b249f3c37f63b2df45b90c4982e68a0a&X-Amz-SignedHeaders=host&actor_id=72137328&key_id=0&repo_id=111583593&response-content-disposition=attachment%3B%20filename%3Dscrcpy-win64-v2.5.zip&response-content-type=application%2Foctet-stream)
- [scrcpy-win32bit-v2.5.zip (32位)](https://objects.githubusercontent.com/github-production-release-asset-2e65be/111583593/ae901e92-dd1b-48b9-8b13-2c8639721fdb?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=releaseassetproduction%2F20240727%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240727T171525Z&X-Amz-Expires=300&X-Amz-Signature=3ceebe85815c0e792a56870bf0439f38c0d535db803873e39ce8cd9b45e9d934&X-Amz-SignedHeaders=host&actor_id=72137328&key_id=0&repo_id=111583593&response-content-disposition=attachment%3B%20filename%3Dscrcpy-win32-v2.5.zip&response-content-type=application%2Foctet-stream)

或者[scrcpy的官网](https://scrcpy.net/download/)
然后解压
或者你可以从包管理器安装它，比如Chocolatey：

```cmd
choco install scrcpy
choco install adb    # if you don't have it yet
```

或者Scoop：

```cmd
scoop install scrcpy
scoop install adb    # if you don't have it yet
```

## 运行

确保你的设备满足[先决条件](#先决条件)。
Scrcpy是一个命令行应用程序：它主要用于从具有命令行参数的终端执行，所有的设置与配置都是通过命令行完成的。
首先，手机与电脑通过USB数据线连接并在手机上点击授权调试，在你解压得到的文件目录下打开终端，或双击scrcpy目录中的 `open_a_terminal_here.bat` 然后输入命令
例如，直接通过USB投屏（没有任何参数）：

```cmd
scrcpy
```

详细的命令行参数文档可以在终端内运行：

```cmd
scrcpy --help
```

或者查阅[官方文档](https://github.com/Genymobile/scrcpy/blob/master/README.md)

下面介绍常用的使用USB投屏方法和使用WiFi投屏的方法：

### USB投屏

1. 手机通过USB数据线连接到电脑
2. 在手机上点击授权调试
3. 在终端中输入 `scrcpy` 命令

<span style="text-decoration: underline;">_使用USB投屏的时候数据线如果被拔掉，画面也会跟着消失_</span>

### WiFi投屏

Scrcpy 使用 adb 与设备通信，将你的设备和电脑用数据线连接起来，并且 adb 支持通过 TCP/IP 连接到设备（设备必须连接与电脑相同的网络）。

<b style="font-size: 14px">自动配置</b>

参数 `--tcpip` 允许自动配置连接。这里有两种方式。

如果 adb TCP/IP（无线）模式在某些设备上不被启用（或者你不知道IP地址），用USB连接设备，然后运行：

```cmd
scrcpy --tcpip    # 无需其他参数
```

这将会自动寻找设备IP地址，启用TCP/IP模式，然后在启动之前连接到设备。

这样，在下次使用无线投屏时，你可以直接运行 `scrcpy -e` 来直接连接，<span style="text-decoration: underline;">_若手机重启后需要重新执行一次上面的操作才可以重新无线投屏_</span>

对于传入的 adb 连接，如果设备（在这个例子中以 192.168.1.1 为可用地址）已经监听了一个端口（通常为 5555），运行：

```cmd
scrcpy --tcpip=192.168.1.1       # 默认端口是5555
scrcpy --tcpip=192.168.1.1:5555
```

<b style="font-size: 14px">手动配置</b>

或者，可以通过 `adb` 使用手动启用TCP/IP链接：

1. 将设备连接到电脑
2. 确保设备和电脑连接的是同一WiFi
3. 打开 `设置 > WLAN > *你连接到的WiFi后面的更多信息 > IP地址` ，也可以执行以下的命令：

```cmd
adb shell ip route | awk '{print $9}'
```

4. 启用设备的网络 adb 功能： `adb tcpip 5555`
5. 拔掉数据线
6. 连接到你的设备： `adb connect DEVICE_IP:5555` （把 `DEVICE_IP` 换成上面你获得到的设备的IP地址）

## 特殊情况

假如你已经使用过一次无线投屏，下次再使用USB投屏的时候，画面会消失，这是因为scrcpy默认使用的是无线投屏，所以需要重新连接USB数据线，然后再次点击授权调试，再输入 `scrcpy` 命令即可。

或者你可以输入 `scrcpy -d` 命令以使用USB投屏。

你需要启用 `开发者选项 -> USB调试（安全设置）` 才可以进行鼠标点击和键盘输入。

## FAQ

### 常见问题疑难解答

这里是一些常见的问题以及他们的状态。

- [常见问题](#常见问题疑难解答)
  - [adb相关问题](#adb相关问题)
    - [找不到adb](#找不到adb)
    - [设备未授权](#设备未授权)
    - [未检测到设备](#未检测到设备)
    - [已连接到多个设备](#已连接多个设备)
    - [adb版本之间冲突](#adb版本之间冲突)
    - [设备断开连接](#设备断开连接)
  - [控制相关问题](#控制相关问题)
    - [鼠标和键盘不起作用](#鼠标和键盘不起作用)
    - [特殊字符不起作用](#特殊字符不起作用)
  - [客户端相关问题](#客户端相关问题)
    - [效果很差](#效果很差)
    - [Wayland相关的问题](#wayland相关的问题)
    - [KWin compositor 崩溃](#kwin-compositor-崩溃)
  - [崩溃](#崩溃)
    - [异常](#异常)
  - [Windows命令行](#windows命令行)

### adb相关问题

scrcpy执行 `adb` 命令来初始化和设备之间的连接。如果 `adb` 执行失败了，scrcpy就无法工作

在这个情况下，将会输出这个错误：

```cmd
ERROR: "adb get-serialno" returned with value 1
```

这通常不是 scrcpy 的bug，而是你的环境的问题。

要找出原因，请执行以下操作：

```cmd
adb devices
```

#### 找不到adb

你的 `PATH` 中需要能访问到 `adb` 。
在Windows上，当前目录会包含在 `PATH` 中，并且 `adb.exe` 也包含在发行版中，因此它应该是开箱即用的（直接解压就可以）。

#### 设备未授权

```cmd
error: device unauthorized.
This adb server's $ADB_VENDOR_KEYS is not set
Try 'adb kill-server' if that seems wrong.
Otherwise check for a confirmation dialog on your device.
```

连接时，在设备上应该会打开一个弹出窗口。 你必须点击授权 USB 调试。

#### 未检测到设备

```cmd
error: no devices/emulators found
```

确认已经正确启用 [adb debugging](https://developer.android.com/tools/adb?hl=zh-cn#Enabling)。
如果你的设备没有被检测到，你可能需要一些 [驱动](https://developer.android.com/studio/run/oem-usb.html) (在 Windows上)。

#### 已连接多个设备

如果连接了多个设备，你将遇到以下错误：

```cmd
error: more than one device/emulator
```

你必须提供要镜像的设备的标识符：

```cmd
scrcpy -s 01234567890abcdef
```

注意，如果你的设备是通过 TCP/IP 连接的， 你将会收到以下消息：

```cmd
adb: error: more than one device/emulator
ERROR: "adb reverse" returned with value 1
WARN: 'adb reverse' failed, fallback to 'adb forward'
```

这是意料之中的（由于旧版安卓的一个bug），但是在这种情况下，scrcpy会退回到另一种方法，这种方法应该可以起作用。

#### adb版本之间冲突

```cmd
adb server version (41) doesn't match this client (39); killing...
```

同时使用多个版本的 `adb` 时会发生此错误。你必须查找使用不同adb版本的程序，并在所有地方使用相同版本的adb。

你可以覆盖另一个程序中的adb二进制文件，或者通过设置ADB环境变量来让 scrcpy 使用特定的adb二进制文件。

```cmd
set ADB=/path/to/your/adb
scrcpy
```

#### 设备断开连接

如果 scrcpy 在警告“设备连接断开”的情况下自动中止，那就意味着adb连接已经断开了。

请尝试使用另一条USB线或者电脑上的另一个USB接口。

### 控制相关问题

#### 鼠标和键盘不起作用

在某些设备上，您可能需要启用一个选项以允许 模拟输入。 在开发者选项中，打开：

`USB调试 (安全设置) 允许通过USB调试修改权限或模拟点击`

#### 特殊字符不起作用

可输入的文本被限制为ASCII字符。也可以用一些小技巧输入一些带重音符号的字符，但是仅此而已。

### 客户端相关问题

#### 效果很差

如果你的客户端窗口分辨率比你的设备屏幕小，则可能出现效果差的问题，尤其是在文本上
。
为了提升降尺度的质量，如果渲染器是OpenGL并且支持mip映射，就会自动开启三线性过滤。

在Windows上，你可能希望强制使用OpenGL：

```cmd
scrcpy --render-driver=opengl
```

你可能还需要配置缩放行为

#### Wayland相关的问题

在Linux上，SDL默认使用x11。可以通过SDL_VIDEODRIVER环境变量来更改视频驱动：

```cmd
export SDL_VIDEODRIVER=wayland
scrcpy
```

在一些发行版上 (至少包括 Fedora)， `libdecor` 包必须手动安装。

#### KWin compositor 崩溃

在Plasma桌面中，当 scrcpy 运行时，会禁用compositor。

一种解决方法是， 禁用 ["Block compositing"](https://github.com/Genymobile/scrcpy/issues/114#issuecomment-378778613)。

### 崩溃

#### 异常

可能有很多原因。一个常见的原因是您的设备无法按给定清晰度进行编码：

```cmd
ERROR: Exception on thread Thread[main,5,main]
android.media.MediaCodec$CodecException: Error 0xfffffc0e
...
Exit due to uncaughtException in main thread:
ERROR: Could not open video stream
INFO: Initial texture: 1080x2336
```

或者

```cmd
ERROR: Exception on thread Thread[main,5,main]
java.lang.IllegalStateException
        at android.media.MediaCodec.native_dequeueOutputBuffer(Native Method)
```

请尝试使用更低的清晰度：

```cmd
scrcpy -m 1920
scrcpy -m 1024
scrcpy -m 800
```

自 scrcpy v1.22以来，scrcpy 会自动在失败前以更低的分辨率重试。这种行为可以用 `--no-downsize-on-error` 关闭。

你也可以尝试另一种 编码器。

如果您在 Android 12 上遇到此异常，则只需升级到 scrcpy >= 1.18：

```cmd
> ERROR: Exception on thread Thread[main,5,main]
java.lang.AssertionError: java.lang.reflect.InvocationTargetException
    at com.genymobile.scrcpy.wrappers.SurfaceControl.setDisplaySurface(SurfaceControl.java:75)
    ...
Caused by: java.lang.reflect.InvocationTargetException
    at java.lang.reflect.Method.invoke(Native Method)
    at com.genymobile.scrcpy.wrappers.SurfaceControl.setDisplaySurface(SurfaceControl.java:73)
    ... 7 more
Caused by: java.lang.IllegalArgumentException: displayToken must not be null
    at android.view.SurfaceControl$Transaction.setDisplaySurface(SurfaceControl.java:3067)
    at android.view.SurfaceControl.setDisplaySurface(SurfaceControl.java:2147)
    ... 9 more
```

### Windows命令行

从 v1.22 开始，增加了一个“快捷方式”，可以直接在 scrcpy 目录打开一个终端。双击 `open_a_terminal_here.bat` ，然后输入你的命令。 例如：

```cmd
scrcpy --record file.mkv
```

您也可以打开终端并手动转到 scrcpy 文件夹：

1. 按下 `Windows+r` ，打开一个对话框。

2. 输入 `cmd` 并按 `Enter`，这样就打开了一个终端。

3. 通过输入以下命令，切换到你的 _scrcpy_ 所在的目录 （根据你的实际位置修改路径）:

```cmd
cd C:\Users\user\Downloads\scrcpy-win64-xxx
```

然后按 `Enter`

4. 输入你的命令。比如：

```cmd
scrcpy --record file.mkv
```

如果你打算总是使用相同的参数，在 `scrcpy` 目录创建一个文件 `myscrcpy.bat` （启用 显示文件拓展名 避免混淆），文件中包含你的命令。例如：

```cmd
scrcpy --prefer-text --turn-screen-off --stay-awake
```

然后只需双击刚刚创建的文件。

你也可以编辑 `scrcpy-console.bat` 或者 `scrcpy-noconsole.vbs`（的副本）来添加参数。

## 参考

[scrcpy官方中文文档](https://github.com/Genymobile/scrcpy/wiki/README.zh-Hans)
[scrcpy官方文档](https://github.com/Genymobile/scrcpy/blob/master/README.md)

<head>
  <!-- ... -->
  <link
    rel="stylesheet"
    href="https://unpkg.com/@waline/client@v3/dist/waline.css"
  />
  <!-- ... -->
</head>
<body>
  <!-- ... -->
  <div id="waline"></div>
  <script type="module">
    import { init } from 'https://unpkg.com/@waline/client@v3/dist/waline.js';

    init({
      el: '#waline',
      serverURL: 'https://walineforblog-75x7ry1od-loakes-projects.vercel.app/',
    });

  </script>
</body>
