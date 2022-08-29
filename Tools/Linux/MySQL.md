解压

```bash
tar -xzvf ～/Download/mysql-5.7.17-linux-glibc2.5-x86_64.tar.gz
```

移动并修改

```
mv ~/Download/mysql-5.7.17-linux-glibc2.5-x86_64   /usr/local/mysql
```

创建MySQL数据库存放的路径

```
mkdir /usr/local/mysql/data 
```

安装依赖

```
sudo pacman -S numactl
sudo pacman -S ncurses5-compat-libs
```

创建用户组

```
cd /usr/local
sudo groupadd mysql //创建用户组mysql
sudo useradd -r -g mysql mysql //-r参数表示mysql用户是系统用户，不可用于登录系统，创建用户mysql并将其添加到用户组mysql中
sudo chown -R mysql mysql/
sudo chgrp -R mysql mysql/
```

创建配置文件，并设置文件权限（很重要）

```
vim /etc/my.cnf
sudo chmod 644 my.cnf
```

>添加文件内容
>其中skip-grant-tables这个选项可以跳过默认密码。
>初始化的时候不会创建一个临时密码。登录的时候直接回车登录。

```
[client]
default-character-set=utf8
port = 3306
socket = /tmp/mysql.sock

[mysql]
default-character-set=utf8
port = 3306
socket = /tmp/mysql.sock

[mysqld]
character_set_server=utf8
init_connect='SET NAMES utf8'
basedir=/usr/local/mysql
datadir=/usr/local/mysql/data
socket=/tmp/mysql.sock
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid


#不区分大小写
lower_case_table_names = 1
sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
max_connections=5000
default-time_zone = '+8:00'

#开启查询缓存

explicit_defaults_for_timestamp=true`在这里插入代码片`

skip-grant-tables
```

切换到/var/log/创建日志文件mysqld.log并设置读写权限 。

```
cd /var/log
touch mysqld.log
chmod 777 mysqld.log
```

切换到mysql目录下初始化数据库。

```
cd /usr/local/mysql
sudo bin/mysqld --initialize --user=mysql
```



补充部分

```bash
*mkdir -p /var/run/mysqld
*chown -R mysql /var/run/mysqld
```



启动mysql

```
sudo /usr/local/mysql/support-files/mysql.server start
```

登录

> 切换到mysql目录下执行登录命令bin/mysql -u root -p，如果提示输入密码直接回车就行了。前提是在上面的配置文件里面开启了skip-grant-tables这个选项。不然需要输入默认生成的临时密码。

