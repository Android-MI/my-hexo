---
title: Mac下使用gradlew命令注意事项

date: 2017-09-20 13:30:12

urlname: Android-gradlew

updated: 2017-09-20 13:32:22

tags:
- Android

categories: 
- 工作
- Android

comments: true
---

今天 发布代码到 bintray 时，使用 gradlew 命令出现几个小问题，特此记录一下。

### 问题1：

> **`bash: ./gradlew:Permission denied`**

需要改变gradlew的权限，请执行命令解决：`chmod +x gradlew`

### 问题2：

> **`bash:gradlew :command not found`**

Mac 下执行这句指令，需要在**`gradlew`**前加 `./`

例：`./gradlew clean build bintrayUpload -PbintrayUser=用户名 -PbintrayKey=你的 API key -PdryRun=false
`

具体上传步骤，参照了下面的文章：
>1. [Android快速发布项目到jcenter](http://www.jianshu.com/p/1436a2caeddb)
>2. [上传jcenter的“第一次”所遇到的坑 ](http://blog.csdn.net/xingshen58/article/details/51644599)
>3. [Gradle 命令配置](http://blog.csdn.net/u013424496/article/details/52684213)
