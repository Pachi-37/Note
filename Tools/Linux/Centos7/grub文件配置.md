### grub文件配置

定义

- 引导程序

配置文件

- `/etc/default/grub/`
- `/etc/grub.d/`
- `/boot/grub2/grub.cfg`
- `grub2-mkconfig -o /boot/grub2/grub.cfg`
- 进入单用户模式（忘记root密码）



查看

`grub-editenv list`



更改内核引导

`grub-set-default []`



##### 网卡

`rhgb` `quiet`