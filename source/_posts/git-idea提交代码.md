---
title: git/idea提交代码
comments: true
date: 2018-12-04 10:16:40
urlname: git&idea_push
tags:
- git
- 笔记
categories:
- git
---

### git提交

首先安装-[git官网](https://git-scm.com/)
安装一路next即可(其实选项我没砸看)，装好后命令行git看有没有帮助信息，没有就重启试试(git环境变量不用手动配置，事实上我也没在环境变量里看到过，所以不用纠结)

先在托管平台新建项目，进入要上传项目的目录，右键-git bash here

- 先初始化一下项目 `git init`

- 添加远端地址 `git remote add origin 你的仓库地址`
如果在使用命令git remote add时报错：这说明本地库已经关联了一个名叫origin的远程库，此时，可以先用`git remote -v`查看远程库信息,删除已有的GitHub远程库：`git remote rm origin`
再重新添加远端地址<br/>
执行更新项目 `git pull origin master`（有时第一次创建项目也需要执行更新，因为新建项目时会自动添加readme）

- 添加待提交文件到缓冲区 `git add fileName` 如git add aaa.txt，项目嘛一般全部提交 `git add -A`

- commit `git commit -m "提交信息"`

- push `git push origin master`

完成
<br/>
### 可能用到的命令

查看本地变更记录 `git status`
缓存本地文件避免避免拉取的时候被覆盖 `git stash`
拉取最新代码到本地 `git pull --rebase`
缓存的本地变更和拉取的代码合并 `git stash pop`



### idea提交
idea中提交代码还是挺方便的，不过它依赖于git， idea设置好git的应用地址 `file`-`Settings`-`Version Contol`-`git`(直接左上角搜索得了) 
在`path to Git executable`一栏输入或选择你git应用的地址(安装目录下的bin/git.exe，比如我的-E:\office\Gittool\bin\git.exe)
选完点击右边Test测试下，弹窗版本号就ok

环境已经好了，接下来在托管平台新建项目，复制下项目url 
左侧Project栏单击选择要提交的项目/module，再单击工具栏`Vcs`-`Import into Version Contol`- `Create git repository`,选择要提交的项目/module(上面选了这里就会自动定位) 点ok
![创建仓库](http://t1.aixinxi.net/o_1ctrcsf2c6huvgu1jq21fq212pqa.png-w.jpg)

创建好仓库后右键该项目，选`git`-`add`添加到缓冲区
![进缓冲区](http://t1.aixinxi.net/o_1ctrcso9u1fgo9511cv61i071g1ma.png-w.jpg)

继续选`git`-`commit Directory`，填写提交信息commit
最后`git`-`repository`-`push`提交代码，弹窗中会显示待提交的目录，点击该目录右边的origin,在弹出的窗口url一栏下面填写远端地址，
![填写url](http://t1.aixinxi.net/o_1ctresng51trinrh8h01nh9q0fa.png-w.jpg)

确认后origin后会默认出现mater分支==push提交即可(会弹窗输入托管平台的账号及密码)


