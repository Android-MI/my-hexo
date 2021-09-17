---
title: 使用sudo命令进行npm全局安装问题

date: 2017-10-17 13:30:12

urlname: npm-chmod

updated: 2017-10-17 13:32:22

tags:
- Node.js

categories: 
- 工作
- Node.js

comments: true
---

>[转~](http://www.jackpu.com/xiao-chu-macxia-npmquan-ju-an-zhuang-shi-yong-sudoming-ling/)

### 权限问题 Permisiion denied
请不要使用sudo进行安装，关于npm 取消sudo进行全局模块的安装你可以使用下面的命令：
> ``` sudo chmod 777 /usr/local/lib/node_modules ```

如果你看到了下面的报错
```
Error:permission denied.Please apply the write premission to the directory: "/Users/yourUserName"
```
我们建议你运行 `sudo chmod 777 ~` or `mkdir ~/.xtoolkit&chmod 777 .xtoolkit` 来解决

#### #Windows用户安装可能有fsevents模块报错

```
Error:permission denied.Please apply the write premission to the directory: "/Users/yourUserName"
```
首先你应该删除安装路径中`weex-toolkit`中的`node_modules`（路径可以在报错命令行中看到）,删除后运行下面的命令:

```
npm install --no-optional weex-toolkit -g
``` 

#### 旧版本升级报错
首先检查你的npm版本是否大于等于5.0，如果没有，请通过`npm update npm -g`升级。
运行如下命令重新安装
```
rm -rf ~/.xtoolkit
npm un weex-toolkit -g
npm i weex-toolkit -g
```
