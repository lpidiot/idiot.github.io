---
title: linux下mysql安装的一些坑
comments: true
date: 2019-12-10 16:10:10
tags:
- linux
- 环境配置
categories:
---

> 继续上文装环境，这条笔记躺磁盘大半年了有必要贴出来了

### 安装 

直接 `sudo apt install mysql-server` 一般会安装失败安装失败安装失败=  
先更新下apt `sudo apt update`   
再安装 `sudo apt install mysql-server`    
安装过程中会有基佬紫背景的页面弹出来并要求输入用户root的密码，确认输入后就ok了  
&nbsp;

看下mysql是否在运行 `sudo netstat -tap | grep mysql`  
看到有显示就行


### 卸载服务
安装后没卸载干净下次安装会保留以往的部分数据==特别是不会提示你设置密码了  
&nbsp;

删除mysql `sudo apt-get remove mysql-*`  
清理残留数据 `dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P`  

### 不知道密码的情况下修改密码  
1. 看下mysql是否在运行 `sudo netstat -tap | grep mysql` 有显示就行  
2. 查询默认的用户名和密码 `sudo cat /etc/mysql/debian.cnf` 
    - 显示大概是这样子的
    - #Automatically generated for Debian scripts. DO NOT TOUCH!
    - [client]
    - host     = localhost
    - user     = debian-sys-maint
    - password = F64nKZ233QkzL8v9
    - socket   = /var/run/mysqld/mysqld.sock
    - [mysql_upgrade]
    - host     = localhost
    - user     = debian-sys-maint
    - password = F64nKZ233QkzL8v9
    - socket   = /var/run/mysqld/mysqld.sock
    - 其中user代表的用户名,password代表的默认生成的密码
3. 利用默认账号密码登录(-p后面是密码,要把自己的密码放在那里,并且-p跟密码之间无空格)
    - `mysql -u debian-sys-maint -pF64nKZ233QkzL8v9` 
4. 成功进入mysql后原封不动执行下面的语句=
    - mysql> `update mysql.user set plugin="mysql_native_password" where user="root";` 
    - 成功的结果
    - Query OK, 1 row affected (0.00 sec)
    - Rows matched: 1  Changed: 1  Warnings: 0
5. 设置root的密码 `update mysql.user set authentication_string=password('你的密码') where user='root'and Host = 'localhost';`  
6. 退出 exit
7. 重新启动数据库 `sudo service mysql restart` 
8. 用自己刚更新的密码登录 `mysql -u root -p`  
9. 输入密码完事  

&nbsp;
over

### 乱码问题 

先进入mysql控制台看下当前编码情况 `SHOW VARIABLES LIKE 'character%';`   
发现很多都是latin1，改成utf-8  
mysql控制台下=>  
`SET character_set_client = utf8;`  
`SET character_set_connection = utf8;`  
`SET character_set_database = utf8;`  
`SET character_set_results = utf8;`  
`SET character_set_server = utf8;`  
&nbsp;
mysql> `SHOW VARIABLES LIKE 'character%';` 你可以看到全变为 utf8 。  
然而这种方式修改在重启mysql服务后就还原了=  
&nbsp;
要永久生效就得修改配置文件，只有修改my.cnf（一般都是在/etc/my.cnf目录下）文件。注意在Server version: 5.7.17 MySQL Community Server (GPL)版本中，配置文件的位置是：/etc/mysql/mysql.conf.d/mysqld.cnf  

vim打开该配置文件，在[client] [mysql] [mysqld] 下全都追加一条`default-character-set=utf8`  
&nbsp;
这三个section因为环境及版本不同可能有所差异，我的只有[mysqld]  

改完重启服务 `sudo service mysql restart`  
&nbsp;
over