---
title: 在Linux中固定IP地址
date: 2024-09-18T08:04:38.922Z
tags: [教程, Linux]
comments: false
draft: false
---

> 注意，本文所使用的Linux系统为 _CentOS 7 64位_ 版本

## 前言

在Linux中，IP地址是动态分配的，每次重启网络服务后，IP地址可能会发生变化。为了方便管理，我们可以将IP地址固定下来。

首先，我们来了解一下什么是静态IP。静态IP，顾名思义，就是固定不变的IP地址。与之相对的是动态IP，动态IP是由网络服务提供商（ISP）动态分配的，每次连接网络时都可能发生变化。静态IP地址一旦分配给一台设备，就不会轻易改变，这使得它在某些特定的应用场景中具有显著的优势。

那么，为什么我们需要设置静态IP呢？主要有以下几个原因：

- 稳定性：静态IP地址不会随网络连接的变化而改变，这保证了网络连接的稳定性。对于需要长期稳定网络连接的应用，如远程办公、服务器托管、VPN连接等，静态IP是必不可少的。
- 安全性：静态IP地址可以更容易地进行访问控制和安全设置。例如，你可以为特定的IP地址设置防火墙规则，只允许特定的设备访问你的网络。
- 便捷性：对于一些需要频繁访问的设备或服务，使用静态IP地址可以省去每次连接时都需要输入用户名和密码的麻烦。

### 查看网关

首先需要查看一下网关，这是为了确保我们设置的IP地址在同一个网段内
![staticip-step1.png](https://s2.loli.net/2024/09/18/TX4GrHFe3fUv7cp.png)
![staticip-step2.png](https://s2.loli.net/2024/09/18/n31DjFNEgQpASsd.png)
![staticip-step3.png](https://s2.loli.net/2024/09/18/TdW6FGCu4lfeJsI.png)

### 修改ens33网卡的配置信息

使用vi编辑器打开ens33网卡的配置文件：

```bash
vi /etc/sysconfig/network-scripts/ifcfg-ens33
```

![staticip-edit-ens33.png](https://s2.loli.net/2024/09/18/t7oy3lfBxJ4Fche.png)

![staticip-edit-ens33-file.png](https://s2.loli.net/2024/09/18/LaV2jXlsYDvZTG6.png)

修改后的配置信息如下：

```bash
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
UUID=15f45225-a953-4399-b383-7f6e5d1f34df
DEVICE=ens33
ONBOOT=yes
IPADDR=指定的IP地址     #前三位需要与网关的前三位一致，否则无法上网
NETMASK=255.255.255.0
GATEWAY=你的网关
PREFIX=24
DNS1=8.8.8.8
```

_还记得之前查看的网关吗？你指定的IP地址前三位网络号应该与你的网关前三位一致_

**_你设置的固定IP地址应该与网关在<span style="color: red; text-decoration: underline">同一网段</span>，并且不能与局域网内的其他设备冲突。例如，如果网关的IP地址是192.168.1.1，那么你的固定IP地址可以是192.168.1.2到192.168.1.254之间的任意一个地址，但不能是192.168.1.1。_**

修改后按下ESC退出编辑模式，输入 `:wq` 退出并保存修改

配置文件参数说明如下：

![static-ip-tips.png](https://s2.loli.net/2024/09/18/rlU4pSfTWiovx6L.png)

完成修改后，重启网络服务使配置生效：

```bash
systemctl restart network
```

![staticip-restart-network.png](https://s2.loli.net/2024/09/18/5vRpduUcW1rafxm.png)

重启后，使用 `ip addr` 命令查看ens33网卡的IP地址，确认是否已经成功设置为静态IP地址：

```bash
ip addr
```

或者

```bash
ifconfig
```

![staticip-done.png](https://s2.loli.net/2024/09/18/jMfIraYZR9BPXJW.png)

如图所示，ens33网卡的IP地址已经成功设置为静态IP地址。

如果IP地址已经成功设置为静态IP地址，那么你就可以使用这个IP地址进行网络通信了。
