### grub配置文件	

- `/etc/default/grub`
  - 更改引导的内核
    - `grub2-editenv list`  #  查看当前内核信息
    - `grep ^menu /boot/grub2/grub.cfg`  #  查看内核
    - `grub2-set-default [option]`  #  设置引导的内核
    - `GRUB_CMDLINE_LINUX (rhgb / quiet)`  #  删除之后开机打印更加详细的引导信息
- `/etc/grub.d/`
- `/boot/grub2/grub.cfg`
- `grub2-mkconfig -o /boot/grub2/grub.cfg`

##### 进入单用户模式

- 开机选择内核，选择编辑
- 添加`single`(6), `rd.break`(7) 
- 启动
- 挂载
  - `mount -o remount,rw /sysroot`
  - `chroot /sysroot`  #  虚拟目录代替根目录
- 重置密码
  - `echo [passwd] |  passwd --stdin root`
- 为了避免`SELinux`的影响
  - `/etc/selinux/config`