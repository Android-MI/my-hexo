---
title: Git SSH 配置（码云+Github）

date: 2018-01-31 13:30:12

urlname: Git-SSH-Config

updated: 2018-01-31 13:32:22

tags:
- Git

categories: 
- 工作
- Git

comments: true
---

### 码云配置

1.在linux的命令行下，或者是windows上Git Bash命令行窗口中键入
> `ssh-keygen -t rsa -C "xxxx@xx.com"`

2.一直按回车(Enter),不要输入任何密码之类，生成 ssh key pair

3.`ssh-add ~/.ssh/id_rsa`
如果出现 `Could not open a connection to your authentiacation agent` 执行 ```eval `ssh-agent` ```
在执行 `ssh-add ~/.ssh/rsa `成功 `ssh-add l `就有新加的rsa了

4.`cat ~/.ssh/id_rsa.pub `(查看)

5.将公钥复制出来

6.进入码云-个人设置-SSH公钥配置，把复制的东西加进去提交 。
