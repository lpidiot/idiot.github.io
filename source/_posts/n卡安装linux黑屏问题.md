> n卡安装linux黑屏问题

1. 正常开机,在引导菜单时按e进入引导文本编辑页面

2. 找到类似

   ```
    linux	/boot/vmlinuz-5.3.0-53-generic root=UUID=8f96bae5-d8cf-45eb-8a1b-a5f6ac5eb728 ro  quiet splash  $vt_handoff
   ```

3. 在 splash的后面空一格 加入`acpi_osi=! acpi="windows 2009"`(没有splash就在quiet后面加)

4. 按f10保存开机

5. 进入系统后编辑 grub文件 `sudo gedit /boot/grub/grub.cfg`

   再次找到类似` linux	/boot/vmlinuz-5.3.0-53-generic root=UUID=8f96bae5-d8cf-45eb-8a1b-a5f6ac5eb728 ro  quiet  splash  $vt_handoff`的文本

   同样的添加`acpi_osi=! acpi="windows 2009"`

6. 在终端里输入`sudo gedit /etc/default/grub`

7. 在文本末尾添加

   ```
   GRUB_CMDLINE_LINUX_DEFAULT="$GRUB_CMDLINE_LINUX_DEFAULT "'acpi_osi=! acpi_osi="Windows 2009"'
   ```

这样以后就可以正常开机了