---
title: mozjpeg pre-build test failed
date: 2017-11-22 12:00:00
updated: 2017-11-22 14:00:00
urlname: mozjpeg-postinstall
comments: true
tags:
- 日志

categories: 
- 工作 
- 日志
---

>OS X 10.13.1 

`nasm -v`

`NASM version 0.98.40 (Apple Computer, Inc. build 11) compiled on Oct 11 2017`

执行 `npm install`后发现控制台出现如下信息:


```
mozjpeg@4.1.1 postinstall /Applications/XAMPP/xamppfiles/htdocs/bright-cms/node_modules/mozjpeg
node lib/install.js

  ⚠ The `/Applications/XAMPP/xamppfiles/htdocs/bright-cms/node_modules/mozjpeg/vendor/cjpeg` binary doesn't seem to work correctly
  ⚠ mozjpeg pre-build test failed
  ℹ compiling from source
  ✖ Error: autoreconf -fiv && ./configure --disable-shared --prefix="/Applications/XAMPP/xamppfiles/htdocs/bright-cms/node_modules/mozjpeg/vendor" --bindir="/Applications/XAMPP/xamppfiles/htdocs/bright-cms/node_modules/mozjpeg/vendor" --libdir="/Applications/XAMPP/xamppfiles/htdocs/bright-cms/node_modules/mozjpeg/vendor" && make --jobs=4 && make install --jobs=4
Command failed: autoreconf -fiv
    /bin/sh: autoreconf: command not found
    at ChildProcess.exithandler (child_process.js:271:12)
    at emitTwo (events.js:125:13)
    at ChildProcess.emit (events.js:213:7)
    at maybeClose (internal/child_process.js:927:16)
    at Socket.stream.socket.on (internal/child_process.js:348:11)
    at emitOne (events.js:115:13)
    at Socket.emit (events.js:210:7)
    at Pipe._handle.close [as _onclose] (net.js:547:12)
```

> 如下是问题解决的[链接地址](https://github.com/imagemin/imagemin/issues/168)

> 1. Update Xcode command line tools to latest release
> 2. brew install nasm (I was using the bundled OS X version 0.98.40, now using 2.11.08)
> 3. npm cache clean
> 4. npm install

注：PNG reference library: libpng

1. [PNG reference library: libpng](https://sourceforge.net/projects/libpng/)
2. [Mac下ImageMagick安装(libpng)](http://ju.outofmemory.cn/entry/119281)
3. [Mac环境安装imagemagick](http://blog.csdn.net/mrzhangxl/article/details/77914115)
