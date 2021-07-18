# 简单可用Arch Linux安装 第二部分

[![ioitboy](https://pic2.zhimg.com/v2-6f0ce9efeddb7ff83554775d37894b64_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/ioitboy)

[ioitboy](https://www.zhihu.com/people/ioitboy)

沉迷数学，日渐消瘦。

第二部分前面会补全一些比较重要的软件，同时给大家看看我的一些配置，后面主要是关于图形界面的安装。还是尽可能不安装其他的软件，保持系统的干净。

```text
B站配套视频：https://www.bilibili.com/video/BV1uK4y1v7Fy/
```

## 补全软件和配置系统

**远程登录客户机**

- 为了方便远程登录，安装 OpenSSH

```text
# pacman -S openssh
```

- 编辑 sshd_config 文件，并启动 OpenSSH 服务。

```text
# grep -ni rootlogin /etc/ssh/sshd_config
# sed -i '32a PermitRootLogin yes' /etc/ssh/sshd_config
# systemctl start sshd.service
# systemctl enable sshd.service    //开机启动
```

- ssh 登录客户机报错

```text
~ ioitboy@linux ssh root@192.168.50.201
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
SHA256:nnqQGy93ozdGQ27vnRcaJNMfPTiQ4ipPLxTyfY1mLFs.
Please contact your system administrator.
Add correct host key in /home/ioitboy/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /home/ioitboy/.ssh/known_hosts:7
ECDSA host key for 192.168.50.201 has changed and you have requested strict checking.
Host key verification failed.
```

由于第一次使用 192.168.50.201 这个 IP 是在 archiso 上，所以保存 192.168.50.201 这个地址保存了 archiso 的主机标识。新安装客户机已有使用也使用这个地址，配对的密钥不一样。

```text
对外提供 OpenSSH 服务使用的密钥在 /etc/ssh 下
[ioitboy@linux ~]$ ls /etc/ssh
moduli      sshd_config         ssh_host_ecdsa_key.pub  ssh_host_ed25519_key.pub  ssh_host_rsa_key.pub
ssh_config  ssh_host_ecdsa_key  ssh_host_ed25519_key    ssh_host_rsa_key

查看主机密钥指纹
sha56
[ioitboy@linux ~]$ ssh-keygen -lf /etc/ssh/ssh_host_ecdsa_key.pub 
256 SHA256:6K03HAuqQ6UVOlZBaEbAXKWP8WHPu/F9qQh7IYj5ROY no comment (ECDSA)
md5
[ioitboy@linux ~]$ ssh-keygen -l -E md5 -f /etc/ssh/ssh_host_rsa_key.pub
 2048 MD5:6d:6d:86:91:37:12:c6:d4:0e:50:e5:11:48:88:47:19 no comment (RSA)
```

- 删除旧的主机标识

```text
~ ioitboy@linux sed -i '7d' /home/ioitboy/.ssh/known_hosts
```

报错的倒数第三行可以看出旧的主机标识位置

- 重新登录客户机

```text
~ ioitboy@linux ssh root@192.168.50.201
The authenticity of host '192.168.50.201 (192.168.50.201)' can't be established.
ECDSA key fingerprint is SHA256:nnqQGy93ozdGQ27vnRcaJNMfPTiQ4ipPLxTyfY1mLFs.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.50.201' (ECDSA) to the list of known hosts.
root@192.168.50.201's password:
Last login: Wed Jul 29 15:54:37 2020
[root@archlinux ~]#
```

- 创建普通用户

```text
[root@archlinux ~]# useradd -m -s /bin/bash -G wheel ioitboy
[root@archlinux ~]# passwd ioitboy
New password:
Retype new password:
passwd: password updated successfully
```

- 为普通用户设置无密码 sudo

```text
[root@archlinux ~]# visudo
editor:
找到下面行，然后删除注释，保存退出。
# %wheel ALL=(ALL) NOPASSWD: ALL
```

- 为所有用户配置 PS1 变量和命令别名

```text
[root@archlinux ~]# vi /etc/bash.bashrc
editor:
注释下面行
PS1='[\u@\h \W]\$ '

行尾添加下面内容，让后保存退出。
PS1='\W \[\e[36;1m\]\u@\H\[\e[0m\] '
alias ls='ls --color=auto'
alias grep='grep --color=auto'
```

- 检查配置是否生效

```text
[root@archlinux ~]# source /etc/bash.bashrc
~ root@archlinux alias
alias grep='grep --color=auto'
alias ls='ls --color=auto'
```

- 去除普通用户的 PS1 变量覆盖

```text
~ root@archlinux vi /home/ioitboy/.bashrc
editor:
注释下面行然后保存退出。
alias ls='ls --color=auto'
PS1='[\u@\h \W]\$ '
```

**其他软件**

- 安装 polkit

```text
~ root@archlinux pacman -S polkit
```

使普通用户可以执行 systemctl poweroff 之类的电源管理命令。

- 安装 git ，同时进行简单设置。

```text
~ root@archlinux pacman -S git
~ root@archlinux su -l ioitboy
~ ioitboy@archlinux git config --global user.name 'Yang Linfeng'
~ ioitboy@archlinux git config --global user.email ioitboy@qq.com
~ ioitboy@archlinux git config --global core.editor vi
~ ioitboy@archlinux git config --list
user.name=Yang Linfeng
user.email=ioitboy@qq.com
core.editor=vi
```

**配置声音**

- 使用 ALSA 管理声音

```text
~ ioitboy@archlinux sudo pacman -S alsa-utils
~ ioitboy@archlinux sudo aplay -l
**** List of PLAYBACK Hardware Devices ****
card 0: I82801AAICH [Intel 82801AA-ICH], device 0: Intel ICH [Intel 82801AA-ICH]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```

可以看出只有一张声卡和一个设备，所以不需要指定声卡和设备。

调节声音

```text
~ ioitboy@archlinux sudo alsamixer
调节：
MM 标识为静音，使用 m 键取消 Master 和 PCM 的静音，同时调节到 100 这个数值，最后按 Esc 退出。
//我跳过这一步。
```

- 保存声音修改，是使重启依旧有效。

```text
~ ioitboy@archlinux sudo alsactl store
```

我重启后发现字符界面 ioitboy 中的 Master 不是最大值，调到最大值重启就成功了。可能是远程普通用户没权限设置声音，使用 sudo 设置的是 root 用户的声音，最重要把上面的命令执行一次就好。

- 命令行测试声音

```text
$ speaker-test -c 2 -l 1
```



## 图形界面安装

- 最小化安装 xorg 服务

```text
~ ioitboy@archlinux sudo pacman -S xorg-server
```

- 安装 X 服务启动命令工具

```text
~ ioitboy@archlinux sudo pacman -S xorg-xinit
```

- 配置 dwm 窗口管理器启动

```text
~ ioitboy@archlinux cp /etc/X11/xinit/xinitrc ~/.xinitrc
~ ioitboy@archlinux vi .xinitrc
editor:
删除下面内容
twm &
xclock -geometry 50x50-1+1 &
xterm -geometry 80x50+494+51 &
xterm -geometry 80x20+494-0 &
exec xterm -geometry 80x66+0+0 -name login
添加下面内容，然后保存退出。
exec dwm
```

- 安装 DejaVu Sans Mono 终端字体

```text
~ ioitboy@archlinux sudo pacman -S ttf-dejavu
```

- 安装 tmux 增强 st 终端

```text
~ ioitboy@archlinux sudo pacman -S tmux
```

假如直接在 dwm 中使用 st 终端，增加窗口的时候会导致刷新异常。被新窗口覆盖的部分，字符会消失，套上 tmux 可以解决这个问题。

- 简单配置 tmux

```text
~ ioitboy@archlinux echo "set -g status-right ''" > /home/ioitboy/.tmux.conf
```

- 安装程序启动器 dmenu

```text
~ ioitboy@archlinux sudo pacman -S dmenu
```

**安装 dwm 窗口管理器**

- 克隆 dwm 源代码

```text
~ ioitboy@archlinux git clone https://git.suckless.org/dwm
~ ioitboy@archlinux cd dwm
```

- 设置 MANPATH 变量

```text
dwm ioitboy@archlinux vi /etc/profile
editor:
注释下面行
unset MANPATH
在文本末尾添加下面内容，然后保存退出。
export MANPATH=$MANPATH:/opt/man
```

- 编辑 [config.mk](https://link.zhihu.com/?target=http%3A//config.mk/) 文件

```text
dwm ioitboy@archlinux vi config.mk
editor:
把下面内容
PREFIX = /usr/local
MANPREFIX = ${PREFIX}/share/man

X11INC = /usr/X11R6/include
X11LIB = /usr/X11R6/lib
更改为
PREFIX = /opt/dwm
MANPREFIX = /opt/man

X11INC = /usr/include/X11
X11LIB = /usr/include/X11
```

把程序安装在 /opt 目录更加方便管理。

- 创建配置文件并修改

```text
dwm ioitboy@archlinux cp config.def.h config.h
dwm ioitboy@archlinux vi config.h
editor:
把下面的 Mod1Mask 更改为 Mod4Mask ，个人觉得使用 win 键比 alt 键更加好。
#define MODKEY Mod1Mask

把下面
static const char *termcmd[]  = { "st", NULL };
更改为
static const char *termcmd[]  = { "st", "-e", "tmux", NULL };
在 dwm 中使用快捷键启动 st 终端时套上 tmux 。
```

- 编译安装源代码

```text
dwm ioitboy@archlinux sudo make clean install
rm -f dwm drw.o dwm.o util.o dwm-6.2.tar.gz
dwm build options:
CFLAGS   = -std=c99 -pedantic -Wall -Wno-deprecated-declarations -Os -I/usr/include/X11 -I/usr/include/freetype2 -D_DEFAULT_SOURCE -D_BSD_SOURCE -D_POSIX_C_SOURCE=200809L -DVERSION="6.2" -DXINERAMA
LDFLAGS  = -L/usr/include/X11 -lX11 -lXinerama -lfontconfig -lXft
CC       = cc
cc -c -std=c99 -pedantic -Wall -Wno-deprecated-declarations -Os -I/usr/include/X11 -I/usr/include/freetype2 -D_DEFAULT_SOURCE -D_BSD_SOURCE -D_POSIX_C_SOURCE=200809L -DVERSION=\"6.2\" -DXINERAMA drw.c
cc -c -std=c99 -pedantic -Wall -Wno-deprecated-declarations -Os -I/usr/include/X11 -I/usr/include/freetype2 -D_DEFAULT_SOURCE -D_BSD_SOURCE -D_POSIX_C_SOURCE=200809L -DVERSION=\"6.2\" -DXINERAMA dwm.c
cc -c -std=c99 -pedantic -Wall -Wno-deprecated-declarations -Os -I/usr/include/X11 -I/usr/include/freetype2 -D_DEFAULT_SOURCE -D_BSD_SOURCE -D_POSIX_C_SOURCE=200809L -DVERSION=\"6.2\" -DXINERAMA util.c
cc -o dwm drw.o dwm.o util.o -L/usr/include/X11 -lX11 -lXinerama -lfontconfig -lXft
mkdir -p /opt/dwm/bin
cp -f dwm /opt/dwm/bin
chmod 755 /opt/dwm/bin/dwm
mkdir -p /opt/man/man1
sed "s/VERSION/6.2/g" < dwm.1 > /opt/man/man1/dwm.1
chmod 644 /opt/man/man1/dwm.1
```

- 创建软连接方便程序执行

```text
dwm ioitboy@archlinux sudo ln -s /opt/dwm/bin/dwm /usr/local/bin/dwm
```

- 提交所有改变

```text
dwm ioitboy@archlinux git add .
dwm ioitboy@archlinux git commit -m 'Compiling for the first time'
```

**安装 st 终端**

- 克隆 st 源代码

```text
~ ioitboy@archlinux git clone https://git.suckless.org/st
~ ioitboy@archlinux cd st
```

- 编辑 [config.mk](https://link.zhihu.com/?target=http%3A//config.mk/) 文件

```text
st ioitboy@archlinux vi config.mk
editor:
把下面内容
PREFIX = /usr/local
MANPREFIX = $(PREFIX)/share/man

X11INC = /usr/X11R6/include
X11LIB = /usr/X11R6/lib
更改为
PREFIX = /opt/st
MANPREFIX = /opt/man

X11INC = /usr/include/X11
X11LIB = /usr/include/X11
```

- 创建配置文件并修改

```text
st ioitboy@archlinux cp config.def.h config.h
st ioitboy@archlinux vi config.h
editor:
更改下面内容，把终端字体更改为 DejaVu Sans Mono 之后设置渲染参数。
static char *font = "Liberation Mono:pixelsize=12:antialias=true:autohint=true";
更改为
static char *font = "DejaVu Sans Mono:size=10:antialias=true:hinting=true:autohint=false";

删除下面内容，
/* Terminal colors (16 first used in escape sequence) */
static const char *colorname[] = {
        /* 8 normal colors */
        "black",
        "red3",
        "green3",
        "yellow3",
        "blue2",
        "magenta3",
        "cyan3",
        "gray90",

        /* 8 bright colors */
        "gray50",
        "red",
        "green",
        "yellow",
        "#5c5cff",
        "magenta",
        "cyan",
        "white",

        [255] = 0,

        /* more colors can be added after 255 to use with DefaultXX */
        "#cccccc",
        "#555555",
};


/*
 * Default colors (colorname index)
 * foreground, background, cursor, reverse cursor
 */
unsigned int defaultfg = 7;
unsigned int defaultbg = 0;
static unsigned int defaultcs = 256;
static unsigned int defaultrcs = 257;
插入下面内容，这是我使用的配色方案。
/* Terminal colors (16 first used in escape sequence) */
static const char *colorname[] = {

  /* 8 normal colors */
  [0] = "#000000", /* black   */
  [1] = "#fa5355", /* red     */
  [2] = "#67ff4f", /* green   */
  [3] = "#ffff00", /* yellow  */
  [4] = "#4581eb", /* blue    */
  [5] = "#fa54ff", /* magenta */
  [6] = "#33c2c1", /* cyan    */
  [7] = "#ffffff", /* white   */

  /* 8 bright colors */
  [8]  = "#555555", /* black   */
  [9]  = "#fb7172", /* red     */
  [10] = "#67ff4f", /* green   */
  [11] = "#ffff00", /* yellow  */
  [12] = "#6d9df1", /* blue    */
  [13] = "#fb82ff", /* magenta */
  [14] = "#60d3d1", /* cyan    */
  [15] = "#eeeeee", /* white   */

  /* special colors */
  [256] = "#202020", /* background */
  [257] = "#ffffff", /* foreground */
};

/*
 * Default colors (colorname index)
 * foreground, background, cursor
 */
unsigned int defaultfg = 257;
unsigned int defaultbg = 256;
static unsigned int defaultcs = 257;
static unsigned int defaultrcs = 0;

/*
 * Colors used, when the specific fg == defaultfg. So in reverse mode this
 * will reverse too. Another logic would only make the simple feature too
 * complex.
 */
static unsigned int defaultitalic = 7;
static unsigned int defaultunderline = 7;
```

defaultrcs 是指光标被鼠标选中，反转的颜色。

```text
可以使用 http://terminal.sexy/ 这个网站来进行配色，或导入导出终端配置。
我是用的配色基于JetBrains Darcula修改，重点考量了 ls 命令的高亮显示。
```

- 测试 ls 高亮的脚本

```text
cat > show_LS_COLORS.sh << 'EOF'
#!/bin/bash
# For LS_COLORS, print type and description in the relevant color.

IFS=:
for ls_color in $LS_COLORS; do
    color="${ls_color#*=}"
    type="${ls_color%=*}"

    # Add descriptions for named types.
    case "$type" in
    bd) type+=" (block device)" ;;
    ca) type+=" (file with capability)" ;;
    cd) type+=" (character device)" ;;
    di) type+=" (directory)" ;;
    do) type+=" (door)" ;;
    ex) type+=" (executable file)" ;;
    fi) type+=" (regular file)" ;;
    ln) type+=" (symbolic link)" ;;
    mh) type+=" (multi-hardlink)" ;;
    mi) type+=" (missing file)" ;;
    no) type+=" (normal non-filename text)" ;;
    or) type+=" (orphan symlink)" ;;
    ow) type+=" (other-writable directory)" ;;
    pi) type+=" (named pipe, AKA FIFO)" ;;
    rs) type+=" (reset to no color)" ;;
    sg) type+=" (set-group-ID)" ;;
    so) type+=" (socket)" ;;
    st) type+=" (sticky directory)" ;;
    su) type+=" (set-user-ID)" ;;
    tw) type+=" (sticky and other-writable directory)" ;;
    esac

    # Separate each color with a newline.
    if [[ $color_prev ]] && [[ $color != $color_prev ]]; then
        echo
    fi

    printf "\e[%sm%s\e[m " "$color" "$type"

    # For next loop
    color_prev="$color"
done
echo
EOF
```

- 要使用这个脚本需要设置好 LS_COLORS 变量，下面是临时设置变量的方法。

```text
script ioitboy@linux dircolors > /tmp/d
script ioitboy@linux source /tmp/d
```

- 编译安装源代码

```text
st ioitboy@archlinux sudo make clean install
rm -f st st.o x.o st-0.8.4.tar.gz
c99 -I/usr/include/X11  `pkg-config --cflags fontconfig`  `pkg-config --cflags freetype2` -DVERSION=\"0.8.4\" -D_XOPEN_SOURCE=600  -O1 -c st.c
c99 -I/usr/include/X11  `pkg-config --cflags fontconfig`  `pkg-config --cflags freetype2` -DVERSION=\"0.8.4\" -D_XOPEN_SOURCE=600  -O1 -c x.c
c99 -o st st.o x.o -L/usr/include/X11 -lm -lrt -lX11 -lutil -lXft  `pkg-config --libs fontconfig`  `pkg-config --libs freetype2`
mkdir -p /opt/st/bin
cp -f st /opt/st/bin
chmod 755 /opt/st/bin/st
mkdir -p /opt/man/man1
sed "s/VERSION/0.8.4/g" < st.1 > /opt/man/man1/st.1
chmod 644 /opt/man/man1/st.1
tic -sx st.info
7 entries written to /usr/share/terminfo
Please see the README file regarding the terminfo entry of st.
st ioitboy@archlinux
```

- 创建软链接

```text
st ioitboy@archlinux sudo ln -s /opt/st/bin/st /usr/local/bin/st
```

- 提交一次更改

```text
st ioitboy@archlinux git add .
st ioitboy@archlinux git commit -m 'Compiling for the first time'
```

- 下载安装隐藏光标补丁

```text
st ioitboy@archlinux mkdir patches
st ioitboy@archlinux cd patches
patches ioitboy@archlinux curl -O https://st.suckless.org/patches/hidecursor/st-hidecursor-0.8.3.diff
st ioitboy@archlinux patch -i patches/st-hidecursor-0.8.3.diff
patching file x.c
Hunk #6 succeeded at 1690 (offset 1 line).
st ioitboy@archlinux sudo make clean install
```

- 提交补丁的更改

```text
t ioitboy@archlinux git add .
st ioitboy@archlinux git commit -m 'patch st-hidecursor-0.8.3.diff'
```

关闭客户机，开始安装扩展包。

**安装 VirtualBox Guest Additions**

打开客户机设置界面，在光驱中装载 VBoxGuestAdditions.iso

ISO 文件在 C:\Program Files\Oracle\VirtualBox 中，启动虚拟机。

- 查找安装编译扩展包所需要依赖

```text
~ ioitboy@archlinux pacman -Q gcc make linux-headers
gcc 10.1.0-2
make 4.3-3
error: package 'linux-headers' was not found
~ ioitboy@archlinux sudo pacman -S linux-headers
```

- 挂载光驱镜像

```text
~ ioitboy@archlinux sudo mkdir /mnt/optical_disc
~ ioitboy@archlinux sudo mount -t iso9660 /dev/sr0 /mnt/optical_disc
mount: /mnt/optical_disc: WARNING: source write-protected, mounted read-only.
~ ioitboy@archlinux cd /mnt/optical_disc
optical_disc ioitboy@archlinux sudo sh ./VBoxLinuxAdditions.run
Verifying archive integrity... All good.
Uncompressing VirtualBox 6.1.12 Guest Additions for Linux........
VirtualBox Guest Additions installer
Copying additional installer modules ...
Installing additional modules ...
VirtualBox Guest Additions: Starting.
VirtualBox Guest Additions: Building the VirtualBox Guest Additions kernel
modules.  This may take a while.
VirtualBox Guest Additions: To build modules for other installed kernels, run
VirtualBox Guest Additions:   /sbin/rcvboxadd quicksetup <version>
VirtualBox Guest Additions: or
VirtualBox Guest Additions:   /sbin/rcvboxadd quicksetup all
VirtualBox Guest Additions: Building the modules for kernel 5.7.10-arch1-1.
VirtualBox Guest Additions: Running kernel modules will not be replaced until
the system is restarted
```

- 为了能够正常的自动适应屏幕，还有一个软件必须要装。

```text
optical_disc ioitboy@archlinux sudo pacman -S libxrandr
```

如何启动图形界面？

```text
登录创建的普通用户，执行命令 startx
```

## 结语：

过程真的很漫长很漫长，我是说看这篇文章。我确信自己已经尽可能的说清楚我懂得知识，如果如果熟悉整个过程，操作起来倒不用很长时间，相对与哪些不熟悉而且真正难装的系统。

最后也没什么了，希望大家在 GNU/Linux 的世界玩得开心。