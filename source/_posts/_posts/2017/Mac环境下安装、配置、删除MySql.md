---
title: Mac下安装、配置、删除 mysql

date: 2017-11-09 13:30:12

urlname: Java-Mysql

updated: 2017-11-09 13:32:22

tags:
- Java

categories: 
- 工作
- JavaWeb

comments: true
---

转： [mac安装mysql的两种方法（含配置)][http://www.jianshu.com/p/fd3aae701db9](http://www.jianshu.com/p/fd3aae701db9)

## 1.修改默认密码
> 前提： 配置好 mysql 环境变量

``` 
// 配置 MySQL 环境变量
$ vi ~/.bash_profile

export MYSQL_HOME=/usr/local/mysql
export PATH=$PATH:$MYSQL_HOME/bin

$ source ~/.bash_profile
```
```
// 需要 MySQL 服务在运行状态执行
$ cd /usr/local/mysql/bin

$ SET PASSWORD FOR 'root'@'localhost' = PASSWORD('123456');
```
## 2.MySql 的启动，停止和状态

```
$ cd /usr/local/mysql

// 启动
$ sudo ./support-files/mysql.server start

// 重启
$ sudo support-files/mysql.server restart

// 停止
$ sudo support-files/mysql.server stop

// 检查 MySQL 运行状态
$ sudo support-files/mysql.server status

```

## 3.查看数据库
```
$ cd /usr/local/mysql/bin
$ ./mysql -u root -p
输入修改后的密码

// 使用数据库
mysql> use mysql

Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| test               |
+--------------------+
4 rows in set (0.00 sec)

```
---
### mysql 备注：
**a.删除 mysql：**
```sudo rm /usr/local/mysql
sudo rm -rf /usr/local/mysql*
sudo rm -rf /Library/StartupItems/MySQLCOM
sudo rm -rf /Library/PreferencePanes/My*
vim /etc/hostconfig  (and removed the line MYSQLCOM=-YES-)
rm -rf ~/Library/PreferencePanes/My*
sudo rm -rf /Library/Receipts/mysql*
sudo rm -rf /Library/Receipts/MySQL*
sudo rm -rf /var/db/receipts/com.mysql.*
```
**b.更改 mysql 安装目录所属用户与用户组:**
```
cd /usr/local
sudo chown -R root:wheel mysql
```

**c.切换到 mysql 安装目录并执行初始化命令并记录生成的临时 root 密码:**
```
cd /usr/local/mysql
sudo bin/mysqld --initialize --user=mysql
```

**d.mysql的 Root 权限设置**
>转链接：http://www.jianshu.com/p/d926d66a4d60


