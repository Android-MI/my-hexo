---
title: Git常见安装问题

date: 2018-01-31 13:30:12

urlname: Git-Questions

updated: 2018-01-31 13:32:22

tags:
- Git

categories: 
- 工作
- Git

comments: true
---

### 配置
配置用户名(提交时候会引用)
> ```git config --global user.name "yourusername" ```  『--global表示是全局的』

#### 配置邮箱
> ```git config --golbal user.email "youremail"```

冲突merge使用版本 ```git config --global merge.tool "kdiff3"``` (没装kdiff3忽略本行)

#### 让Git不要管Windows/Unix换行符转换的事
> ```git config --global core.autocrlf false```

### 编码配置
#### 避免git gui中的中文乱码
> ```git config --global gui.encoding utf-8```

#### 避免git status显示的中文名乱码
> ```git config --global core.quotepath off```

#### windows区分大小写设置
>```git config --global core.ignorecase false```

------
### 使用命令： git status 查看状态
`git init`  初始化仓库
`git add . ` 将所有文件(除去忽略的文件，添加到仓库中)
`git commit -am ` “添加注释” 提交文件到仓库

------
### 推送到远程仓库
1.复制远程仓库地址 `git@gitee.com:xxxxx/xxxx.git` 添加远程仓库
> ` git remote add origin git@gitee.com:xxxxx/xxxx.git`

2.查看分支
> `git branch`
`git push -u[-f] origin master` (-f表示强制更新)

提交代码到远程仓库
>1. 先执行下  `git pull` 【拉取一下】
>2. 执行 `git push -u origin master`
>3. 如果还报错的话 `git push -u -f origin master` 【强制替换更新】

------
——主流的开发模式支线开发 主干发布——
查看本地分支`git branch`
查看远程分支`git branch -r`
— 创建分支
`git checkout -b v1.0 origin/master` 【 -b表示创建新的分支 origin/master 表示v1.0在远程 master的基础上 】
发部到远程仓库
`git push origin HEAD -u` 远程会有两个仓库 master v1.0
> `git checkout [master/v1.0] `切换分支
