---
title: linux挂载ntfs硬盘不能正常写入
comments: true
date: 2020-07-01 19:10:10
tags:
- linux
- 环境配置
categories:
---

1inux系统自动挂载该移动硬盘到/media目录下，通过ls -al查看其权限，显示为：drwx------，证明我们可以进入到该盘符目录，但当进一步查看该盘符下的某可执行文件的权限时，发现其为-rw-------，即可以对该文件进行读写操作，但不能执行该文件，通过chmod更改权限也无济于事.解决方法:



首先查看分区

```
sudo fdisk -l
```

```
设备             起点       末尾      扇区   大小 类型
/dev/sdb1        2048  209719295 209717248   100G Microsoft 基本数据
/dev/sdb2   209719296  419436543 209717248   100G Microsoft 基本数据
/dev/sdb3   419436544 1048584191 629147648   300G Microsoft 基本数据
/dev/sdb4  1048584192 1953523711 904939520 431.5G Microsoft 基本数据
```

执行修复,拿sdb1来说

```
sudo ntfsfix /dev/sdb1
```

重新挂载

```
sudo mount /dev/sdb1 /挂载路径
```

再次打开sdb1权限就正常了.



没有ntfsfix指令先安装ntfsprogs

```
sudo apt install ntfsprogs
```



