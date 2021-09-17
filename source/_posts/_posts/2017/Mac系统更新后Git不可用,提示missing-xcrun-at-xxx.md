---
title: Mac系统更新后Git不可用,提示missing-xcrun-at-xxx
date: 2017-11-12 12:00:00
updated: 2017-11-23 14:00:00
urlname: xcode-select-install

tags:
- 日志

categories: 
- 工作 
- 日志
comments: true
---

> 记录于2017-11-13：更新后 MacOS 版本为 `10.13.1`

今天系统升级后，发现原来开发 IDE 里的 git 托管项目，没法`push`和`pull` 操作了，然后看到控制台里提示信息：

>``` xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun```

百度一圈后，找到了解决方案，特摘录一份备份。

据说苹果每个版本更新后都有这样的问题，原因是每次安装更醒后，Xcode 都被卸载了。通过终端重新安装的Xcode命令行工具使用（其实这里安装的是Command Line Tools，Command Line Tools是在Xcode中的一款工具）

## 1 :命令行安装
>``` xcode-select --install ```

按照提示安装完毕即可，安装成功后，重新查看 git 版本信息：
> ``` git version ```

至此，应该就算 OK 了，简单省事。

