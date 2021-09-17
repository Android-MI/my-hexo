---
title: weex开发环境搭建
date: 2017-09-29 12:00:00
updated: 2017-09-29 14:00:00
urlname: weex-toolkit

tags:
- weex

categories: 
- 工作 
- Weex
comments: true
---

**~『 NO. 1 安装依赖 』**

> Weex 官方提供了 weex-toolkit 的脚手架工具来辅助开发和调试。首先，你需要 Node.js 和 [Weex CLi](https://github.com/weexteam/weex-toolkit)。

> ` Node.js ` 安装方式，请移步 [Node.js 安装](http://www.jianshu.com/p/3d7c3f5ecf1f)

安装完成后，可以使用以下命令检测是否安装成功：
> $ `node -v`
> v6.11.3
> $ `npm -v`
> 3.10.10 

通常，安装了 Node.js 环境，npm 包管理工具也随之安装了。

注意: 在 ` weex-toolkit `1.0.8 版本后添加了npm5规范的 ` npm-shrinkwrap.json `用于锁定包依赖，故npm版本<5的用户需要通过` npm i npm@latest -g `
更新一下npm的版本，使用前请确认版本是否正确。

> $`npm install -g weex-toolkit`
$ `weex -v `//查看当前weex版本

weex-toolkit也支持直接升级子依赖，如：
> `weex update weex-devtool@latest `//@后标注版本后，latest表示最新

提示：
如果提示权限错误（*permission error*），使用 ` sudo `关键字进行安装
> $ ` sudo npm install -g weex-toolkit `

安装结束后你可以直接使用 ` weex ` 命令验证是否安装成功，它会显示  ` weex `命令行工具各参数：

![weex 命令行工具各参数.png](http://upload-images.jianshu.io/upload_images/1552105-b1d127f85238eed8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/840)

**~『 NO. 2 初始化 』**

然后初始化 Weex 项目：
>$ ` weex create awesome-project `

执行完命令后，在 ` awesome-project ` 目录中就创建了一个使用 Weex 和 Vue 的模板项目


**~『 NO. 3  开发』**

之后我们进入项目所在路径，`weex-toolkit` 已经为我们生成了标准项目结构。
在 `package.json`中，已经配置好了几个常用的 npm script，分别是：

  * `build`: 源码打包，生成 JS Bundle
  * `dev`: webpack watch 模式，方便开发
  * `serve`: 开启HotReload服务器，代码改动的将会实时同步到网页中

我们先通过`npm install`安装项目依赖。之后运行根目录下的` npm run dev & npm run serve `开启 watch 模式和静态服务器。

然后我们打开浏览器，进入 http://localhost:8080/index.html 即可看到 weex h5 页面。

初始化时已经为我们创建了基本的示例，我们可以在` src/index.vue `中查看。

代码如下所示：

```
<template>
  <div class="wrapper" @click="update">
    <image :src="logoUrl" class="logo"></image>
    <text class="title">Hello {{target}}</text>
    <text class="desc">Now, let's use vue to build your weex app.</text>
  </div>
</template>
<style>
  .wrapper { align-items: center; margin-top: 120px; }
  .title { padding-top:40px; padding-bottom: 40px; font-size: 48px; }
  .logo { width: 360px; height: 156px; }
  .desc { padding-top: 20px; color:#888; font-size: 24px;}
</style>
<script>
  export default {
    data: {
      logoUrl: 'http://img1.vued.vanthink.cn/vued08aa73a9ab65dcbd360ec54659ada97c.png',
      target: 'World'
    },
    methods: {
      update: function (e) {
        this.target = 'Weex'
        console.log('target:', this.target)
      }
    }
  }
</script>
```

>1. 关于 Weex 语法部分，你可以直接参考 [Vue Guide](https://vuejs.org/v2/guide/)
>2. 你可以在 [dotWe](http://dotwe.org/vue/d48fbf8e8b2bb7bf555d0c380902eb37) 写代码并随时预览。
>3. [weex-toolkit 使用说明，请移步官网查看](https://weex.apache.org/cn/guide/tools/toolkit.html)
>4. [Weex Playground 工具](https://weex.apache.org/cn/playground.html)
>5. [Weex Market](https://market.dotwe.org/#7)
>6. [Weex语法支持插件](https://weex.apache.org/cn/guide/tools/plugin.html)

