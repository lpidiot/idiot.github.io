---
title: manjaro开局配置
date: 2020-07-11 20:21:53
comments: true
tags:
- linux
- 环境配置
---

## 基本配置

#### 更换中国源

```
sudo pacman-mirrors -i -c China -m rank
sudo pacman -Syy
```

在第一条命令结束的时候会弹出一个窗口让你选择想要使用的源，选最快的那个就行了。

修改`/etc/pacman.conf`

在文件末尾加上

```
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
```

然后运行这两行命令：

```
sudo pacman -S archlinuxcn-keyring #-S表示安装某一软件
sduo pacman -Syy # -Syy表示将本地的软件与软件仓库进行同步
```

然后就可以更新一下系统：

```
sudo pacman -Syyu	#可以更新系统的一切软件包
```

升级完之后你可能发现你的中文字体变成了口

```
sudo pacman -S wqy-microhei
```

#### 输入法

```
sudo pacman -S fcitx-im    #默认全部安装
sudo pacman -S fcitx-configtool
sudo pacman -S fcitx-sogoupinyin
```

在`~/.xprofile`文件（没有则需要新建）中加入：

```
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```

#### 安装tim

```
pacman -S deepin.com.qq.office
sudo pacman -S gnome-settings-daemon
系统设置->开机或关机->自动启动->添加脚本->输入/usr/lib/gsd-xsettings
```

安装后字体发虚，换wine字体比较麻烦，可以调dpi凑合。

执行下面语句打开wine设置

```
env WINEPREFIX="$HOME/.deepinwine/Deepin-TIM" winecfg
```

 之后会打开图像设置页面 dpi调个120差不多了..太大显示很难受

#### 常用软件

```
sudo pacman -S vim
sudo pacman -S netease-cloud-music
sudo pacman -S wps-office
sudo pacman -S ttf-wps-fonts
sudo pacman -S typora
sudo pacman -S google-chrome
```

#### 安装Aur工具

```
sudo pacman -S yay
```

#### varay图形客户端

```
yay -S v2ray-desktop
```



## 美化(mac向)

终端：

主题商店的完全够用，选一个喜欢/契合主题的的即可，nordic还不错



图标：

```repl
系统设置->图标->获取新的图标->搜索Mojave CT Icon安装
```



dock栏/顶栏

```
sudo pacman -S latte-dock
```

装好后在桌面添加即可



主题：这里提供一个方案

全局中搜索下载McMojave

应用程序风格-窗口装饰选McMojave-light

颜色：oxygen冷色 或 McMojave-light



字体：

默认字体有点糊..

我这里选的Source Code Pro Medium

抗锯齿启用

微调选完全



## 快捷指令

manjaro默认没有ll等命令

编辑`~/.bashrc` 添加alias

```
alias ll='ls -alF'
alias la='ls -A'
alias vi='vim'
```

最后

```
source ~/.bashrc
```

