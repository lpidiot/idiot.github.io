---
title: linux下vscode错误处理
date: 2020-09-11 14:25:22
tags:
 -linux
---

Manjaro Linux使用VSCode的坑

### 1.ENOSPC: System limit for number of file watchers reached

解决方法:

1. cd /etc/sysctl.d/
2. sudo vim 50-max_user_watches.conf
3. 修改内容fs.inotify.max_user_watches = 524288
4. sudo sysctl -p --system





### 2.manjaro使用VSCodeopen in browser 无法设置chrome默认打开
1. vim ~/.vscode/extensions/techer.open-in-browser-2.0.0/out/config.js

2. #修改内容，自行核对  就是把原来的google-chrome修改为google-chrome-stable

   ```
   const chromeItem = {
       description: "Windows, Mac, Linux",
       detail: "A fast, secure, and free web browser built for the modern web",
       label: "Google Chrome",
       standardName: platform === 'win32'
           ? 'chrome'
           : (platform === 'darwin'
               ? 'google chrome'
               : 'google-chrome-stable'),
       acceptName: ['chrome', 'google chrome', 'google-chrome', 'gc', '谷歌浏览器','google-chrome-stable']
   };
   ```

   #还不行，在VSCode中settings.json中修改
   "open-in-browser.default": "google-chrome",
   重启VSCode即可