
---
title: Mac下Tomcat安装和配置

date: 2017-11-02 13:30:12

urlname: Java-Tomcat

updated: 2017-11-02 13:32:22

tags:
- Java

categories: 
- 工作
- JavaWeb

comments: true
---

闲话不说，直接开工：
> 本人机器配置，更新于2017-11-2，以供各位参考
> `Java : 1.8.0_121`
> `Tomcat : 8.5.23`

> 下载地址：
> [Java ](https://www.java.com/zh_CN/download/mac_download.jsp)   
> [Tomcat](http://tomcat.apache.org/download-80.cgi)

Tomcat不区分Linux版和Mac版,但Windows请选择对应的32位或者64位系统 zip 包即可。

## 1. 下载 Tomact
真正的绿色软件，解压，放在指定位置即可。

![Tomcat 8.5.23.png](http://upload-images.jianshu.io/upload_images/1552105-bb4160d3fcab25df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 2. 解压文件
我是放在电脑的 「资源库」文件夹中。
具体位置在：

![解压文件到指定目录.png](http://upload-images.jianshu.io/upload_images/1552105-289fefbb1b80d1d9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 3. 配置环境变量
- 打开控制台，编辑用户环境文件 `.bash_profile`
> ``` vi ~/.bash_profile ```

键入 `i`执行`插入`操作，
- 在打开的文件中，添加 tomcat 路径
> ``` export TOMCAT_PATH=/Users/xiaomi/Library/Tomcat/apache-tomcat-8.5.23/bin ```

- 在原来 `PATH` 后追加 Tomcat 路径，以我本机配置为例（已省略一些其他信息）：

> ``` export PATH=$JAVA_HOME/bin:${TOMCAT_PATH}```

**提示：**  在原 `PATH` 后 使用 `:` 连接  `${TOMCAT_PATH}` 即可。

- **保存退出 `:wq`**， 执行命令使刚才编辑的`.bash_profile`文件生效。
> ``` source ~/.bash_profile ```

配置文件权限：
> ``` cd /Users/(自己的用户目录)/Tomcat/apache-tomcat-8.5.23/bin ```
> ``` sudo chmod +x *.sh ```

## 4.启动 Tomcat，验证配置是否正确
> ```startup.sh ``` // 启动 tomcat
> // 执行后即可访问 http://localhost:8080/
> ``` shutdown.sh ```  // 关闭 tomcat


![tomcat 启动.png](http://upload-images.jianshu.io/upload_images/1552105-a885363f62cd4ba8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

也许你还想点『 Server Status 』按钮看看服务器状态，但你马上发现不行，你没有设置管理员的用户名/密码，它不让你看。


![查看服务器状态.png](http://upload-images.jianshu.io/upload_images/1552105-288ed84048622f7c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

对于这种情况，我们看到
tomcat 7.0需要将manager-gui, manager-script, manager-jmx, manager-status, admin-gui, admin-script 这些全写上，故编辑
> ``` ../Tomcat/apache-tomcat-8.5.23/conf/tomcat-users.xml ```

在文件里加入下面👇配置（用户名和密码自定义设置，我写的都是 admin）,

> ```<role rolename="manager-gui"/>```
> ```<role rolename="manager-script"/>```
>```<role rolename="manager-jmx"/>```
>```<role rolename="manager-status"/>```
>```<role rolename="admin-gui"/>```
>```<role rolename="admin-script"/>```
>```<user username="admin" password="admin" roles="manager-gui,manager-script,manager-jmx,manager-status,admin-gui,admin-script"/>  ```

重启 tomcat 后，这时候点击『 Server Status 』入下图所示：

![Server Status.png](http://upload-images.jianshu.io/upload_images/1552105-34950d1440a00b36.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 以上内容，整理自其他博文以便自己记录和查看，也希望能帮到他人。
