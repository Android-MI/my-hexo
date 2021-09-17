---
title: 上传library到自己创建的maven仓库
date: 2017-11-22 12:00:00
updated: 2017-11-22 14:00:00
urlname: upload-library-to-maven
comments: true

tags:
- Library

categories: 
- 工作 
- Library
---

根目录build添加

```

buildscript {

repositories {

jcenter()

}

dependencies {

classpath 'com.android.tools.build:gradle:2.2.2'

classpath 'com.novoda:bintray-release:0.3.4'

}

```


需要上传Library的build添加

```

apply plugin: 'com.novoda.bintray-release'

publish {

userOrg = ''      //bintray注册的用户名

groupId = ''        //compile引用时的第1部分groupId

artifactId = ''    //compile引用时的第2部分项目名

publishVersion = '1.0.0'    //compile引用时的第3部分版本号

desc = ''

website = ''

}

```

最后打开Termainal执行命令

发布到bintary 命令

` ./gradlew clean build bintrayUpload -PbintrayUser=用户名 -PbintrayKey=自己KEY -PdryRun=false`
