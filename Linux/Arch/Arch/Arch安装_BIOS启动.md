# 安装系统

## 更新系统时间

```bash
timedatectl set-ntp true
```



## 更新镜像源

```bash
vim /etc/pacman.d/mirrorlist
```

在最上方没有#的行插入

```bash
Server = https://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch   #使用中科大的源
Server = http://mirrors.aliyun.com/archlinux/$repo/os/$arch #阿里源
```

保存退出后执行

```bash
pacman -Syy
```

## 分区

`lsblk`查看磁盘

```bash
NAME	MAJ:MIN	RM   SIZE RO TYPE MOUNTPOINT
loop0	  7:0    0 534.8M  1 loop /run/archiso/sfs/airootfs
sda       8:0    0    20G  0 disk
sr0		  11:0	 1	 651M  0 rom /run/archiso/bootmnt
```

将sda分为一个区

```bash
fdisk /dev/sda
```

按n，然后一路回车，然后按w

格式化分区

```bash
mkfs.ext4 /dev/sda1
```

挂载分区到/mnt目录

```bash
mount /dev/sda1 /mnt
```

## 安装系统

```bash
pacstrap /mnt base base-devel linux linux-firmware
```

# 配置系统

## Fstab

```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

## Chroot

Change root到新安装的系统

```bash
arch-chroot /mnt
```

## 安装vim

```bash
pacman -S vim
```

## 时区

配置ArchLinux时间

```bash
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

设置硬件时间

```bash
hwclock --systohc --utc
```

## 修改编码格式

```bash
vim /etc/locale.gen
```

找到`en_US.UTF-8 UTF-8`和`zh_CN.UTF-8 UTF-8`，把前面的#删除，保存退出

```bash
locale-gen	#重新生成locale
echo LANG=en_US.UTF-8 > /etc/locale.conf	#生成locale.conf文件
```

## 创建主机名

```bash
echo Arch > /etc/hostname	#Arch可自定义
```

编辑hosts文件

```bash
vim /etc/hosts
```

添加以下配置

```bash
127.0.0.1	localhost.localdomain	localhost
::1			localhost.localdomain	localhost
127.0.0.1	Arch.localdomain		Arch
```

## 配置网络组件

```bash
pacman -S dhcpcd
systemctl enable dhcpcd		#开机自动联网
```

## 设置ROOT用户

```bash
passwd	#直接回车输密码
```

## 安装Bootloader

```bash
pacman -S grub  #安装grub
grub-install --target=i386-pc /dev/sda 
grub-mkconfig -o /boot/grub/grub.cfg    #生成配置文件
```

# 完成

```bash
exit	#退出系统
umount -R /mnt	  #取消挂载
reboot	  #重启
```

