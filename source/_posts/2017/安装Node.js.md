---
title: 安装 Node.js
date: 2017-09-29 12:00:00
updated: 2017-09-29 14:00:00
urlname: node-install
comments: true

tags:
- Node.js

categories: 
- 工作 
- Node.js
---

**~『 NO. 1 』**

> 安装 `Node.js` 方式多种多样，最简单的方式是在 [Node.js 官网](https://nodejs.org/en/) 下载可执行程序直接安装即可。

对于 Mac，可以使用 [Homebrew](http://brew.sh/) 进行安装：
``` brew install node ```

> 更多安装方式可参考 [Node.js 官方信息](https://nodejs.org/en/download/)

安装完成后，可以使用以下命令检测是否安装成功：
> $ node -v
> v6.11.3
> $ npm -v
> 3.10.10 

通常，安装了 Node.js 环境，npm 包管理工具也随之安装了。

**~『 NO. 2 』**

> npm版本<5的用户需要通过`npm i npm@latest -g `更新一下npm的版本，使用前请确认版本是否正确。


**~『 NO. 3 』**

> 国内开发者可以考虑使用淘宝的 npm 镜像 —— [cnpm](https://npm.taobao.org/) 安装 weex-toolkit

> $ npm install -g cnpm --registry=https://registry.npm.taobao.org




