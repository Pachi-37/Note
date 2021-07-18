## Vmware使用技巧

1. 增加物理内存
   - 虚拟机关机
   - 编辑虚拟机内存
2. 添加硬件设备
3. 控制权限切换
4. 关机
5. 结束虚拟机任务
   - CTRL +  Alt + Ins   等于  CTRL  +  Alt  + delete
6. 网络区域
   - 桥接——独立模式
   - （）共享路由器
7. 虚拟机BIOS设置   开机按F2
8. 安装 Vmware  Tools 分辨率
9. IOS 镜像文件
10. 删除虚拟机
11. 快照管理



### Linux终端介绍

- tty  控制台终端（CTRL+shift+Alt +F2——6）

- pts  虚拟机终端 (ctrl shift T)  alt 1/2 (切换)

  - ```
    ps -axu | grep pts
    ```

  - 伪终端   ：ssh相关工具，显示出来的

### shell提示符

​	【用户@主机名    当前目录】提示符    root 为 #   普通用户为$

### Bash  Shell  基本语法

命令【选项】（【参数】）【选项的值】（【参数的值】）

常见选项（参数）：-h    --help     ；特点：选项样子为 :   -字母   或  --加单词





### 实验快照标准

1. 配置好静态IP
2. 关闭IP table防火墙
3. 关闭selinux

### 服务器开机后自动开机

BIOS

1. integrated Per ipharals
2. super IO Device
3. Restore On AC Power Loss
   - Last state（断电）
   - Power On（不断电）