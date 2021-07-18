# 网络管理

##### 网络状态查看

- `net-tools`
  - ` route -n`
    - 查看网关
    - `-n`参数不解析主机名
  - `mii-tool ens33`
    - 查看网络连接情况
  - `ifconfig`
    - 网卡的表示默认使用`eth`开头
    - 第一块网卡`eth0`(网络接口)
    - `Centos7`使用一致性网络设备命名方式

> `eno1`：板载网卡 `ens33`：PCI-E网卡 `enp0s3` ：无法获取物理信息的PCI-E网卡

注：为了操作方便将网卡转换为统一的名称

> 网卡的命名规则受到`biosdevname` `net.ifnames`两个参数的影响

```bash
#  编辑`/etc/default/grub`，添加`bisodevname=0` `net.ifnames=0`
#  更新grub
grub2-mkconfig -o /boot/grub2/grub.cfg
#  重启
reboot
```

||`biosdevname`|`net.ifnames`|网卡名称|
| ---- | ---- | ---- | ---- |
| 默认 | 0 | 1 | `ens33` |
|组合1|1|0|`em1`|
| 组合2 | 0 | 0 | `eth0` |

```bash
# inet ：网卡的IP地址。
# netmask ：网络掩码。

# ether: (硬件mac地址)

# lo本地环回一般设置为`127.0.0.1`
```



- `iproute2`				

`ip`

- `ip address is`
  - `ifconfig`		
- `ip link set dev eth0 up`
  - `ifup eth0`
- `ip addr add 10.0.0.1/24 dev eth1`
  - `ifconfig eth1 10.0.0.1 netmask 255.255.255.0`
- `ip route add 10.0.0/24 via 192.168.0.1`
  - `route add 10.0.0.0 netmask 255.255.255.0 gw 192.168.0.1`



### 网络故障排除

- `ping`

  - `traceroute`

    - ```bash
      traceroute -w 1 www.baidu.com
      #  跟踪数据包，最多等待1s
      ```

  - `mtr`

- `nslookup`

  - ```bash
    nslookup 域名
    #  解析域名对应的IP地址
    ```

- `telnet`

  - ```bash
    telnet 域名/IP 端口
    #  跟踪对应端口是否
    
    ^]
    quit
    #  退出程序
    ```

- `tcpdump`

  - ```bash
    tcpdump -i any -n port 80
    #  抓包工具
    #  -i any  所有网卡里面的数据包 -n IP方式显示 port指定端口
    #  host 10.0.0.1指定主机
    #  -w显示的信息另存到其他文件里面
    ```

- `netstat`

  - ```bash
    netstat -ntpl
    #  查看服务的监听地址
    #  n：显示IP t:tcp p:显示进程 l:服务显示
    ```

- `ss`



### 网络配置文件`Sysv` `systemd` 

- `service network start|stop|restart`

- `chkconfig -list network`
- `systemctl list-unit-files NetworkManager.service`
- `systemctl start|stop|restart NetworkManager`
- `systemctl enable|disable NetworkManager`

> 两套服务的脚本 `network`(服务器较多) `NetworkManager.service` 使用其中一个

#### 禁用其中一个服务脚本

```bash
chkconfig --list network
chkconfig --level 2345 network off

systemctl disable NetworkManager
```

### 网络配置文件

- `ifcfg-`
- `/etc/hosts`
- 静态IP配置

```bash
BOOTPROTO=none
IPADDR=
NETMASK=
GATEWAY=
DNS1=  #  可以设置3个
```

- 主机名

```bash
hostname
hostname 【】
#  临时生效
hostnamectl set-hostname 【】
#  长时间生效
vim /etc/hosts
127.0.0.1 新的主机名
```

