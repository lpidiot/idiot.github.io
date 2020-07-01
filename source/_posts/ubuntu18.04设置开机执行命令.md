前言

- Ubuntu18.04 默认是没有 /etc/rc.local 这个文件的，需要自己创建
- systemd 默认读取 /etc/systemd/system 下的配置文件，该目录下的文件会链
- 接/lib/systemd/system/下的文件。执行 ls /lib/systemd/system 你可以看到有很多启动脚本，其中就有我们需要的 rc.local.service

查看rc.local.service文件内容

```
sudo vim /lib/systemd/system/rc.local.service
```

```
#  SPDX-License-Identifier: LGPL-2.1+
#
#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or modify it
#  under the terms of the GNU Lesser General Public License as published by
#  the Free Software Foundation; either version 2.1 of the License, or
#  (at your option) any later version.

# This unit gets pulled automatically into multi-user.target by
# systemd-rc-local-generator if /etc/rc.local is executable.
[Unit]
Description=/etc/rc.local Compatibility
Documentation=man:systemd-rc-local-generator(8)
ConditionFileIsExecutable=/etc/rc.local
After=network.target

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
RemainAfterExit=yes
GuessMainPID=no

```

一般正常的启动文件主要分成三部分

- [Unit] 段: 启动顺序与依赖关系
- [Service] 段: 启动行为,如何启动，启动类型
- [Install] 段: 定义如何安装这个配置文件，即怎样做到开机启动

可以看出，rc.local.service 它少了 Install 段，也就没有定义如何做到开机启动，所以显然这样配置是无效的。 因此我们就需要在后面帮他加上 [Install] 段，可以发现rc.local.service是rc-local.service文件的链接文件，所以我们只需要修改rc-local.service文件即可：

```
sudo vim /lib/systemd/system/rc.local.service
```

添加

```
[Install]  
WantedBy=multi-user.target  
Alias=rc-local.service
```

在`/etc/`目录下面创建`rc.local`文件，赋予执行权限，

```
sudo  touch /etc/rc.local
chmod +x /etc/rc.local
```

`/etc/rc.local` 文件添加如下内容：

```
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.
echo "测试脚本执行成功" > /usr/local/test.log
exit 0
```

systemd 默认读取 `/etc/systemd/system` 下的配置文件，将`/lib/systemd/system/rc.local.service` 链接到`/etc/systemd/system`目录

```
 sudo ln -s /lib/systemd/system/rc.local.service /etc/systemd/system/
```



> 不想链接的话也可以直接新建 在/etc/systemd/system下新建rc-local.service文件
>
> ```
> sudo vim /etc/systemd/system/rc-local.service
> ```
>
> 把以下内容复制到该文件
>
> ```
> [Unit]
> Description=/etc/rc.local Compatibility
> ConditionPathExists=/etc/rc.local
>  
> [Service]
> Type=forking
> ExecStart=/etc/rc.local start
> TimeoutSec=0
> StandardOutput=tty
> RemainAfterExit=yes
> SysVStartPriority=99
>  
> [Install]
> WantedBy=multi-user.target
> ```



启动服务

```
sudo systemctl enable rc-local
```

启动服务并检查状态

```
sudo systemctl start rc-local.service
sudo systemctl status rc-local.service
```

重启后检查test.log文件是否已经存在



参考

[https://blog.csdn.net/github_38336924/article/details/98183253](https://blog.csdn.net/github_38336924/article/details/98183253)	[https://www.jianshu.com/p/79d24b4af4e5](https://www.jianshu.com/p/79d24b4af4e5)

 