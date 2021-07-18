# 服务管理

### 服务管理工具

- `service`
  - `/etc/init.d/network`
- `systemctl`
  - `/usr/lib/systemd/system/`

##### 系统启动的级别

```bash
chkconfig --list
#  0：关机无法被kill -9  init 0
#  6：重启 1：单用户 2:无网络的多用户 3：字符模式 5：图形化
```



### `SELinux`

- `MAC` —— 强制访问控制； `DAC` —— 自主访问控制
- 相关命令
  - `getenforce`
  - `/usr/sbin/sestatus`
  - `ps -Z and ls -Z and id -Z`
- 关闭
  - `setenforce=0`
  - `/etc/selinux/sysconfig`

> 足够安全，但是会降低服务器的性能

##### 修改配置文件

`/etc/selinux/config`



### 内存与磁盘管理

- ##### 内存与磁盘使用率

  - `free`
    - `-m/-g`
  - `top`
  - `fdisk`
    - `-l`
  - `df`
    - `-h`
      - 可以看到挂载的目录
  - `du`
    - `du`和`ls`区别
      - `du`实际占用空间

> 创建空洞文件 `dd if=/dev/zero bs=4M count= seek= of=`



- ##### `ext4` 文件系统

- ##### 磁盘配额使用

- ##### 磁盘分区与挂载

- ##### 交换分区（虚拟内存）

- ##### `RAID`

- ##### 逻辑卷

- ##### 系统状态

