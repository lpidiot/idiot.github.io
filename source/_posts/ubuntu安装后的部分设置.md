## 修改软件源

默认的软件源一般是官方的软件源,在国内速度实在不行.

1. 备份配置文件

   ```
   cp -a /etc/apt/sources.list /etc/apt/sources.list.bak
   ```

2. 修改source.list文件 将原本的http://archive.ubuntu.com以及http://security.ubuntu.com替换掉

   ```  
   sed -i "s@http://*.archive.ubuntu.com@http://mirrors.huaweicloud.com@g"  /etc/apt/sources.list
   sed -i "s@http://.*security.ubuntu.com@http://mirrors.huaweicloud.com@g" /etc/apt/sources.list
   ```

> [网易开源镜像](https://mirrors.163.com/) /  [清华大学开源镜像站](https://mirrors.tuna.tsinghua.edu.cn/) / [华为开源镜像站](https://mirrors.huaweicloud.com/)



##  设置sudo免密码

普通用户执行sudo需要输入密码 而作为个人使用免密没啥风险

​	``` sudo visudo ```

在`%sudo ALL=(ALL:ALL) ALL`下添加`$USER ALL=(ALL) NOPASSWD: ALL`

> \# Allow members of group sudo to execute any command
> `%sudo ALL=(ALL:ALL) ALL`
> `$USER ALL=(ALL) NOPASSWD: ALL`

> **$USER** 变量改为你的用户名，另外 **visudo** 命令就是直接修改 /etc/sudoers 文件。



## 修改 HOSTNAME

HOSTNAME 就是主机名，用于其他人或其他设备识别这台主机，`$HOSTNAME` 取一个自己喜欢的名字表示个性。

```
hostnamectl set-hostname $HOSTNAME
hostname -F /etc/hostname
```



## 配置静态 IP

使用 `ifconfig` 命令查看网卡名，我这里是 `enp3s0f1`，
然后根据网卡名修改文件 `sudo vim /etc/netplan/02-network-manager-enp3s0f1.yaml` 

也有的只有一个`01-network-manager-all.yml`的文件,自行确认

```
# Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
  ethernets:
          enp3s0f1:
                  addresses: [192.168.0.123/24]
                  gateway4: 192.168.0.1
                  nameservers:
                        addresses: [119.29.29.29, 223.5.5.5, 8.8.8.8]
```

> 注意：严格保持结构层次，一般人修改 IP:192.168.0.123 后面的 123 为 2~253 中的某个数就行了。



执行以下命令使配置即时生效：

```
sudo netplan apply
```

这里同时配置了 DNS 和 ipv4 地址，可不用再修改 /etc/systemd/resolved.conf 文件单独配置 DNS。 当然单独配置 DNS 的方法还是介绍一下：

`sudo vim /etc/systemd/resolved.conf`

```
[Resolve]
DNS=119.29.29.29 223.5.5.5 8.8.8.8
```

重启服务生效：

```
systemctl restart systemd-resolved.service
```



## 将个人文件夹转移到其他分区

> 在 Windows 上有很多人会将默认在 C 盘的个人文件夹 ( Downloads/Documents/Music/Videos 等) 转移至 D 盘，
>
> * 一部分是减少对系统盘读写资源的占用
> * 一部分是减少系统盘空间的占用
> * 还有一部分是避免系统坏了 C 盘资料恢复的麻烦
>
> Linux 上我主要是为了避免重装系统时备份个人文件夹的麻烦，所以将个人文件夹转移到其他分区。
>
> UEFI 方式安装系统，我一般分四个区（/boot/efi、/、/DATA、swap），非常有必要将个人文件夹转移到存储个人数据的 /DATA 分区下，重装系统不格式化 /DATA 分区，省去备份资料的麻烦。



先备份系统文件，然后修改：

```
cd /home/$USER/.config/
cp -a user-dirs.dirs{,.bak}
vim user-dirs.dirs
```

删除默认值，添加下面自定义值：

```
XDG_DOWNLOAD_DIR="/DATA/Downloads"
XDG_TEMPLATES_DIR="/DATA/Templates"
XDG_PUBLICSHARE_DIR="/DATA/Public"
XDG_DOCUMENTS_DIR="/DATA/Documents"
XDG_MUSIC_DIR="/DATA/Music"
XDG_PICTURES_DIR="/DATA/Pictures"
XDG_VIDEOS_DIR="/DATA/Videos"
XDG_DESKTOP_DIR="/DATA/Desktop"
```

修改文件后要想马上生效还要运行 `source user-dirs.dirs` 否则只能重登用户生效。



## Alias 提高工作效率

`sudo vim /etc/bashrc`

```
alias c='clear'  # 快速清屏
alias vi='vim'
alias up='sudo apt update'
alias upg='sudo apt upgrade'
alias dup='sudo apt dist-upgrade'
alias fix='sudo apt -y --fix-broken install'   # 修复依赖，可简写为：apt -y -f install
alias arm='sudo apt -y autoremove'
```

使用 source 命令立即生效：

```bash
source /etc/bashrc
```

或者

```bash
. /etc/bashrc
```

> 都不行的话先sudo su到root用户再用source



## 软件

#### Eddy 可直接点击 DEB 包即可安装软件的小工具

```
sudo apt -y install com.github.donadigo.eddy
```



#### wps

先去官网下载deb包直接安装

启动后提示字体缺失 出现提示的原因是因为WPS for Linux没有自带windows的字体，只要在Linux系统中加载字体即可。

[字体文件]( https://pan.baidu.com/s/1UgOF-xK3ygBp7S2mEVEJXg ) 提取码: s6pi

1. 下载完成后，解压并进入目录中，继续执行：

   ```
   sudo cp * /usr/share/fonts
   ```

2. 执行以下命令,生成字体的索引信息：

   ```
   sudo mkfontscale
   sudo mkfontdir
   ```

3. 运行fc-cache命令更新字体缓存

   ```
   sudo fc-cache
   ```

4. 重启wps



方法二：

```
sudo cp * /usr/share/fonts/wps-office 
```

即可



#### Markdown 编辑器：[Typora](https://typora.io/#linux) + [Pandoc](https://github.com/jgm/pandoc/releases/tag/2.3.1)

```
wget -qO - https://typora.io/linux/public-key.asc | sudo apt-key add -
sudo add-apt-repository 'deb https://typora.io/linux ./'
sudo apt update
sudo apt -y install typora

wget https://github.com/jgm/pandoc/releases/download/2.3.1/pandoc-2.3.1-1-amd64.deb
sudo dpkg -i pandoc-2.3.1-1-amd64.deb
```



#### deepin-wine-for-ubuntu

[deepin-wine-for-ubuntu](https://gitee.com/wszqkzqk/deepin-wine-for-ubuntu)



#### nodejs

```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```





转自 [Pancras Lao](https://me.csdn.net/laopengcheng) 

[原文](https://blog.csdn.net/laopengcheng/article/details/82861760)

