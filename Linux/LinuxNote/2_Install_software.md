# Install software

### 软件包管理器

软件安装、卸载、依赖关系

`rpm`包格式

- 软件名称、软件版本、系统版本、平台
- rpm
  - `-q`  查询软件包
  - `-i`  安装软件包
  - `-e`  卸载软件包

```bash
mount  /dev/sr0 /mnt
cd /mnt/Packages
```

```bash
#  查看已经安装的软件
rpm -qa
```



### `yum`

yum源

##### 常用命令

- `install`
- `remove`
- `list|grouplist`
- `update`



### 源码编译

- 下载
- 解压

```bash
tar -zxf
```

- 编译

```bash
cd
./configure --prefix=///
make -j2
make install
```

- 安装



### 升级内核

查看内核版本

```bash
uname -r
```

升级内核版本

​	