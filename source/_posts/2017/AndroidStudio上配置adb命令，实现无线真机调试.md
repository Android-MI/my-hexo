---
title: AndroidStudio上配置adb命令，实现无线真机调试

date: 2017-09-19 13:30:12

urlname: Android-ADB

updated: 2017-09-19 13:32:22

tags:
- Android

categories: 
- 工作
- Android

comments: true
---

##  1. 配置 adb 命令

一直想在AndroidStudio的Terminal中 输入 adb 命令，但是终究没有尝试。今天心血来潮想试试无线调试，可是在控制台输入`adb devices` 后，缺提示 `bash: adb: command not found` 。好吧，让我来先配置一下环境变量（`Mac OS 10.12.6` ` jdk1.8.0_121`）。

>1.Mac下打开终端：Launchpad -> 其他 -> 终端
>2.输入：`touch .bash_profile `
>3.打开：`open -e .bash_profile`
>4.保存：`source .bash_profile`

其中进行第3步，打开的 **.bash_profile** 文件，文件的路径一定要改成你自己电脑中的具体路径。

我电脑中配置：  
```
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_121.jdk/Contents/Home

export PATH=$JAVA_HOME/bin:$PATH:/Users/xiaomi/Library/Android/sdk/tools/:/Users/xiaomi/Library/Android/sdk/platform-tools/

export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM into a shell session *as a function*
```
**注意：** *PATH* 变量中的 Android/sdk/tools 路径。

执行 `source .bash_profile` 后，
输入 `adb` 命令，可见控制台输出：
```
Android Debug Bridge version 1.0.39
Revision 5943271ace17-android

global options:
 -a         listen on all network interfaces, not just localhost
 -d         use USB device (error if multiple devices connected)
 -e         use TCP/IP device (error if multiple TCP/IP devices available)
 -s SERIAL
     use device with given serial number (overrides $ANDROID_SERIAL)
 -p PRODUCT
     name or path ('angler'/'out/target/product/angler');
     default $ANDROID_PRODUCT_OUT
 -H         name of adb server host [default=localhost]
 -P         port of adb server [default=5037]
 -L SOCKET  listen on given socket for adb server [default=tcp:localhost:5037]

general commands:
 devices [-l]             list connected devices (-l for long output)
 help                     show this help message
 version                  show version num
......
```
OK~ 你该明白了吧。

##  2. AS 中手动实现无线真机调试

无线真机调试很简单，无需插件，无需 Root，使用插件反而会将这个流程复杂化。先放上 *纯流程版* ，方便阅读之后快速查阅，

### 纯流程版
```
1. 将手机与电脑连接在同一局域网内
2. 手机用线连接电脑，控制台输入命令adb devices, 有设备编号为连接成功
3. 拔手机线，控制台输入命令 adb tcpip 5555，将TCP模式在 5555 端口启动，无任何输出为成功启动
4. 控制台输入命令 adb connect 192.168.56.101:5555
其中：192.168.56.101 为手机在局域网的 ip 地址，输出连接成功
此时无线连接已经成功，正常调试即可
```
### 详细版

打开 **命令行终端** ，键入` adb devices `，这个命令会输出所有连接到这台电脑上的设备，每个设备有一个独一无二的序列号。
见图 : 

![图片.png](http://upload-images.jianshu.io/upload_images/1552105-22014e24ffc65c2e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)

**进行无线连接**

输入命令`adb tcpip 5555`，这个命令的作用是打开手机的 TCP 模式，并且将其绑定到 5555 接口。其中，5555 端口是一个习惯使用的端口，就像 MySql 一般使用 3306 端口一样，也可以随意指定，只要不产生端口冲突即可。

这条命令执行后没有任何输出，但是手机会出现一次，类似于与电脑断线并且重新插线的反应，代表执行成功。
打开成功之后，就可以拔掉手机数据线了。

接下来执行连接命令，但是首先我们需要进入手机 WIFI 网络详情，找到此时手机 WIFI 中的 IP 地址。接下来就可以执行连接命令了，连接命令为 adb connect 手机 IP 地址: TCP 绑定的端口。

例如，我手机的 IP 地址是 192.168.31.93，之前 TCP 模式绑定的端口为 5555，此时我需要执行的连接命令为 `adb connect 192.168.31.93:5555`
此时控制台输出 connected to 192.168.31.93:5555，表示无线连接成功。

![无线连接.png](http://upload-images.jianshu.io/upload_images/1552105-82345073af59d522.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)

TCP 模式一旦开启，只在手机重启时才会关闭，关闭后如果还需使用需要重新开启。断网重连，换 WIFI，不会关闭，只要保持手机电脑在统一 WIFI 下就不需要重新开启。

不过如果手机一旦断网，或者切换 WIFI，与电脑的无线连接会立即断开，如果需要重新连接，重新执行一次 ` adb connect ` 命令就好。

### 调试
在项目中，直接点击 **run**，选择连接的设备即可。

![连接手机调试](http://upload-images.jianshu.io/upload_images/1552105-062796b8693c088d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)

然后，就可以开心的调试了。

## 3. 补充：连接多台设备

使用` adb devices ` 命令，可以得到一个已连接设备的序列号表，一次连接多台设备跟连接一台设备流程类似，通过 『**序列号指定设备** 』即可。

![模拟器和手机同时连接.png](http://upload-images.jianshu.io/upload_images/1552105-e077378d8ef5293b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)

例如，需要进行 TCP 模式开启，`adb -s f87c75bb tcpip 5555 `，但是与电脑建立连接的 adb connect 命令不需要加序列号，因为 IP 地址本来就相当于是序列号了。

然后，查看手机连接的IPv4地址，比如我的是：192.168.0.200
执行 `adb connect 192.168.0.200:5555`

![图片.png](http://upload-images.jianshu.io/upload_images/1552105-c5e2b5412dd95c07.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)

接下来，请开始你的调试吧。

> 个人整理，难免有错误纰漏，欢迎指正。
