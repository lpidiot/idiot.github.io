---
title: linux下jdk/tomcat的安装配置
comments: true
date: 2019-12-10 15:57:17
tags: 
- linux
- 环境配置

categories:
---

> 新买了服务器，这次换ubuntu的系统镜像了。重新装了遍环境发现还是记下比较好== (图床挂了,不加图了)

### jdk

我电脑存了以前下的jdk，所以直接传过去得了=  
&nbsp;

先安装传文件用的lrzsz -&emsp;`apt install lrzsz`  

看下有没装好-&emsp;`dpkg -l lrzsz`&emsp; 出现版本号就完事了  

上传文件 `rz -y` 弹出文件视图选择上传（文件存放在当前目录） 

先到usr把目录建好 `cd /usr/local`  `mkdir java` 

到创好的目录操作吧 `cd java`  

解压下之前的jdk压缩包`tar -zxvf /root/jdk1.8.gz ./`  
&nbsp;

配置环境变量(按实际的文件目录来填=)=> 

`vim /etc/profile` 插入以下环境  
`export JAVA_HOME=/usr/java/jdk1.8`  
`export JRE_HOME=$JAVA_HOME/jre`  
`export CLASSPATH=.:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/rt.jar`  
`export PATH=$PATH:$JAVA_HOME/bin`  

保存退出  

更新下配置 `source /etc/profile`  

java -version没问题就完事了  
&nbsp;

顺便，现在linux都预装了openjdk，以上配置之后还是会显示openjdk，切换下就好  

`sudo update-alternatives --install /usr/bin/java java /jdk绝对路径/bin/java 300`  

over

### tomcat  
这里能方便查看 [tomcat镜像](https://mirrors.tuna.tsinghua.edu.cn/apache/tomcat)  
&nbsp;

安装 `wget https://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-9/v9.0.29/bin/apache-tomcat-9.0.29.tar.gz` 

解压到自己的目录(习惯/usr/local/java/tomcat) `tar -zxvf apache* /usr/local/java/tomcat`  

名字太长了改下吧= `mv apache* tomcat-9.0.29`  
&nbsp;

配置环境变量`vim /etc/profile`  
添加下面的语句  
`export TOMCAT_HOME=/usr/local/java/tomcat/tomcat-9.0.29`  
`export PATH=$PATH:$TOMCAT_HOME/bin`  

保存退出，更新下配置`source /etc/profile`

over