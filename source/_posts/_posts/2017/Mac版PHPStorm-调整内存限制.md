---
title: Mac版PHPStorm-调整内存限制
date: 2017-12-12 13:00:00
updated: 2017-12-12 16:00:00
urlname: phpstorm-vmoptions

tags:
- 日志

categories: 
- 工作 
- 日志
comments: true
---

## 调整方法

> 参考链接 https://segmentfault.com/a/1190000003960160
```
# 用的是 mac osx，编辑 phpstorm 的启动配置文件，其他平台根据情况选择:
sudo vim /Applications/PhpStorm.app/Contents/bin/phpstorm.vmoptions

# 修改参数，根据具体需要修改即可，一般修改  -Xmx(即最大可占内存)即可
-Xms512m
-Xmx2048m
-XX:MaxPermSize=350m
-XX:ReservedCodeCacheSize=240m
-XX:+UseCompressedOops
```

修改 Webstorm 同理：
```
-Xms512m
-Xmx2048m
-XX:MaxPermSize=350m
-XX:ReservedCodeCacheSize=240m
-XX:+UseCompressedOops 
```
