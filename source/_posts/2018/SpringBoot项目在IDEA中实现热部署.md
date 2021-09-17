---
title: SpringBoot项目在IDEA中实现热部署

date: 2018-01-01 13:30:12

urlname: springboot-hot

updated: 2018-07-30 11:00:12

tags:
- Springboot

categories:
- 工作
- Springboot

comments: true
---

> 版本： `Intellij IDEA 2017.3 `

## 1. 引入插件
引入热加载的插件，springboot 1.3开始就有的...

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
```
project 中添加`spring-boot-maven-plugin`,主要在eclipse中起作用，idea不需要加此配置。
SpringBoot 项目的话，应该是有此配置，加 <configuration> 里面的内容即可。

```
<build>
       <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <fork>true</fork>
                </configuration>
            </plugin>
        </plugins>
    </build>
```
## 2. IDEA（2017.3）  配置
1. 点击： `File-> Settings -> Build ,Execution,Deployment -> Compiler `
> Mac版IDEA，使用快捷键 `command + ,` 打开 `Preferences`
> 定位到`-> Build ,Execution,Deployment -> Compiler `

![Compiler.png](https://upload-images.jianshu.io/upload_images/1552105-1d6baae9f115170b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/940)

选中 `Build project automatically`，然后点击  `OK` 保存退出。

2. 使用组合键：`Shift+ALT+Ctrl+/` ，选择`Registry`，回车
> Mac版  `command + option +shift +/`

![Registry-01.png](https://upload-images.jianshu.io/upload_images/1552105-3598a1828697e483.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/740)
![Registry-02.png](https://upload-images.jianshu.io/upload_images/1552105-ca65db85c2ae5a1b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/940)

搜索 `complier.automake.allow.when.app.running` ，找到后，勾选 ☑️ 退出即可。

3. 禁用浏览器缓存
按F12（更多工具---->开发者工具），找到network，勾选Disable Cache。



