# Arch虚拟机安装（UEFI驱动）

### 准备

1. VMware虚拟机
2. Arch镜像（ios）
   - ArchLinux官方镜像（2020-06）

### 安装

- ##### Vmware虚拟机设置

  - 驱动设置
    - 虚拟机设置
    - 选项——高级
    - 固件类型选择UEFI
  - 网络设置
    - 选择NAT模式
  - 建立磁盘文件

### 安装Arch（命令模式）

- 改变字体大小

  - setfont /usr/share/kbd/consolefont/LatGrKyr-12x22.psfu.gz

- 分盘

  - fdisk  -l				//查看磁盘情况

  - fdisk  (dev/sda)        //括号内情况根据上条命令而定（非虚拟机）

  - n	                          //建立分区

  - 具体步骤

    - n				
    - <Enter>        //选择数字
    - <Enter>        //选择起始位置
    - +内存大小     //+512M   +  1G

  - 格式化硬盘

    - mkfs.fat -F32	/dev/sda1
    - mkfs.ext4           /dev/sda2
    - mkswap           /dev/sda3

  - 选择并编辑镜像源
    vim /etc/pacman.conf	//编辑pacman配置文件
        

    ```
    Color           			 	//去掉#号似的pacman具有颜色提醒的功能
    ```

    ​    :w                				//保存配置

    vim /etc/pacman.d/mirrorlist		//或者直接在命令行中编辑此文件

    ```
     qa    						//vim宏编辑技巧，qa开始录制宏，宏名为a
        		gg		    		//到最开始一行
        		/^\n+Enter  		//找到第一个空行进入
          	/China+Enter  //找到China所在行
          	Shift+v     		//尽量可视行编辑模式
          	j           			//选择China行及下面一行
          	d           			//剪切这两行
          	gg          			//到最开始一行
          	/^\n+Enter 		 //找到第一个空行进入
          	k           //上移一行
          	p           //粘贴剪切的两行
          	q           //退出宏录制
        @a      		//多次执行录制的宏a，将所有的中国镜像源放在最开始
        :wq     	//保存退出
    ```

    vim /etc/pacman.d/mirrorlist		//或者直接在命令行中编辑此文件


### 挂载并安装Linux

```
mount /dev/sda2 /mnt  //挂载mnt分区
mkdir /mnt/boot       //建立boot目录
mount /dev/sda1 /mnt/boot   //挂载boot分区

swapon  /dev/sda3   //打开交换

pacstrap /mnt base linux linux-firmware //安装linux
genfstab -U /mnt >> /mnt/etc/fstab      //设置linux
```



### 配置Linux

arch-chroot /mnt              //进入安装好的系统

```
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime    //选择中国上海作为时区
hwclock --systohc  		   //同步系统时间
```

pacman -S vim   		      //安装文本编辑器

```
vim /etc/locale.gen  		 //编辑语言
  en_US.UTF-8 UTF-8 		 //将注释#号去掉,保存退出
```



```
pacman -S vim   		      //安装文本编辑器
vim /etc/locale.gen  		 //编辑语言
  en_US.UTF-8 UTF-8 		 //将注释#号去掉,保存退出
```

locale-gen	#重新生成localeecho LANG=en_US.UTF-8 > /etc/locale.conf	#生成locale.conf文件

vim /etc/vconsole.conf		 //键盘配置

```
KEYMAP=us 				//键盘设置，默认就是us  对于所支持的可以在命令行中输入

keycode 1 = Caps_Lock

keycode 58 = Escape    //这两行可以将Esc和CapsLock两个键互换
```



### 网络

vim /etc/hostname 		  //编辑网络名字文件  

```
 arch       						   //取网络名字arch
```

vim /etc/hosts				  //网络设置

```
  127.0.0.1	  localhost
  ::1	      	localhost
  127.0.1.1	  arch.localdomain	arch    //使用上一步设置的网络名字arch

```

passwd  					  //更改root密码

```
pacman -S grub efibootmgr intel-ucode os-prober  //安装一个BootLoader
mkdir /boot/grub 						//创建一个文件夹
grub-mkconfig > /boot/grub/grub.cfg //生成启动配置文件到文件夹
```

uname -m  								  //确认一下系统的架构，目前多数是x86_64
grub-install --target=x86_64-efi --efi-directory=/boot

```
pacman -S wpa_supplicant dhcpcd 	 // **重要** 安装好网络部件wpa_supplicant及动态分配ip工具dhcpcd，其他软件可以在之后有网络进行按需安装

```

exit  		  //回到之前的系统
reboot 		 //安装好后可以进行重启

### 重启后配置linux的用户及联网功能

用root登入系统继续配置linux
df -lh   //查看系统安装磁盘容量信息

```
ip link //查看网络连接状况
ip link set ens33 up  //打开虚拟机的网卡
```

dhcpcd  //运行动态分配ip
ping baidu.com  //连接百度进行上网测试
ip addr //其作用类似于ifconfig
ip route //其作用显示当前实际在使用的网卡端口状态和路由网关信息
pacman -S netctl  //安装网络管理软件来管理网卡
cp /etc/netctl/examples/ethernet-dhcp /etc/netctl/my_dhcp_profile    //将例子中的有线连接配置文件复制到目录下并改名为my_dhcp_profile
vim /etc/netctl/my_dhcp_profile  //修改配置文件

```
  Interface=ens33   //配置连接网络名
  Connection=ethernet   //为有线连接
  IP=dhcp   //自动分配ip地址
```

netctl start my_dhcp_profile  //启动网络连接服务
netctl enable my_dhcp_profile //设置开机启动网络连接服务
pacman -S openssh //安装openssh服务
systemctl start sshd.service //启动openssh服务
systemctl enable sshd.service //设置开机启动ssh服务
vim /etc/ssh/sshd_config //编辑sshd配置文件

  # Authentication:   //运行root用户进行ssh登入

  LoginGraceTime 2m  //将注释#号去掉

  #PermitRootLogin prohibit-password

  PermitRootLogin yes   //添加一行
  StrictModes yes      //将注释#号去掉
useradd -m -G wheel winnerwood //添加一个用户在wheel用户组中
passwd winnerwood  //给这个用户添加密码

***

 pacman -S     sudo      //安装sudo命令

ln -s /usr/bin/vim /usr/bin/vi //编辑管理员权限时候可以用vim替代vi命令
visudo  //编辑sudo文件

%wheel ALL=(ALL) ALL //将注释#去掉，让这个组中用户可以执行任何命令。保存退出

### 安装一些常用软件

采用新建的用户winnerwood进行操作
sudo pacman -Syyu  //更新一下系统
sudo pacman -S man //manual命令
sudo pacman -S base-devel  //软件开发工具集
sudo pacman -S neofetch   //显示计算机信息的软件
neofetch        //观察运行效果

### 安装fish和（oh-my-fish）

```
sudo pacman -S fish
sudo pacman -S git
# with git
$ git clone https://github.com/oh-my-fish/oh-my-fish
$ cd oh-my-fish
$ bin/install --offline
```

修改默认shell

```
取代bash，设为默认shell
sudo usermod -s /bin/fish username
或者
chsh -s /bin/fish
或者
chsh -s `which fish`
```





修改默认文本编译器为Vim

```bash
vim ~/.profile
export EDITOR=/usr/bin/vim
# 可以注释掉nano

vim ~/.bashrc
export EDITOR=
export VISUAL=
```

