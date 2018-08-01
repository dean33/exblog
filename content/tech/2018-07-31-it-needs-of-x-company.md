---
title: 'IT needs of X-Company '
author: ''
date: '2018-07-31'
slug: it-needs-of-x-company
categories: []
tags: []
---

This passage is meant to record the essential information technology needs when a small company wants to leverage the internet's power.


**Non-production IT needs:**  
- 邮件系统：Mail  
- 文档协作：Git  
- 目录管理：LDAP  
- *开发管理：持续集成与部署CI/CD*  
- *运行监测：Zabbix*
- ERP：odoo^[[odoo](www.odoo.com)]或其他开源ERP^[[值得考虑的九大开源ERP系统](http://os.51cto.com/art/201804/570668.htm)]  
  
  
**Production IT needs:**  
- 官方网站：静态web系统  
- 业务系统：业务架构、动态web系统  
- *数据资产：OLTP、OLAP、数据安全*   



**IT Management needs:**  
- 容器技术：Docker    
- *配置管理：CMDB*  

## 操作记录 ##


### 安装CentOS7     
下载 CentOS-7-x86_64-DVD-1804.iso ->   [CentOS.org](http://isoredirect.centos.org/centos/7.5.1804/isos/x86_64/), [mirror@Aliyun](http://mirrors.aliyun.com/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-1804.iso)

> CentOS-7-x86_64-DVD-1804.iso This DVD image contains all the packages that can be installed using the installer. This is the recommended image for most users.^[[README](http://mirrors.aliyun.com/centos/7/isos/x86_64/0_README.txt)]



### 常用命令  

**升级系统**  

> <font color='blue'>[root@hoster ~]#</font> **yum** -y update 

**查看版本号**  

> <font color='blue'>[root@hoster ~]#</font> **uname** -r   
3.10.0-327.el7.x86_64  

> <font color='blue'>[root@hoster ~]#</font> **cat** /etc/redhat-release      
CentOS Linux release 7.5.1804 (Core)            

**查看CPU信息**  

> <font color='blue'>[root@hoster ~]#</font> cat /proc/cpuinfo   
<font color='blue'>[root@hoster ~]#</font> lscpu  

**修改主机名**  

> <font color='blue'>[root@hoster ~]#</font> **sysctl** kernel.hostname=your_hostname

**yum搜索程序**  

> <font color='blue'>[root@hoster ~]#</font> **yum** search ifconfig  


**重启系统**  

> <font color='blue'>[root@hoster ~]#</font> **shutdown** -r now  
>Linux centos重启命令：  
　　1、reboot  
　　2、shutdown -r now 立刻重启(root用户使用)  
　　3、shutdown -r 10 过10分钟自动重启(root用户使用)  
　　4、shutdown -r 20:35 在时间为20:35时候重启(root用户使用)  
*如果是通过shutdown命令设置重启的话，可以用shutdown -c命令取消重启*  
　Linux centos关机命令：  
　　1、halt 立刻关机  
　　2、poweroff 立刻关机  
　　3、shutdown -h now 立刻关机(root用户使用)  
　　4、shutdown -h 10 10分钟后自动关机  

**重启网络服务**  

> <font color='blue'>[root@hoster ~]#</font> **systemctl** restart network


**同步时间**  

> <font color='blue'>[root@hoster ~]#</font> **yum** -y install ntpdate  
<font color='blue'>[root@hoster ~]#</font> **ntpdate** 0.cn.pool.ntp.org  
 1 Aug 16:40:02 ntpdate[1229]: step time server 5.103.139.163 offset -31455.587035 sec    
<font color='blue'>[root@hoster ~]#</font> **systemctl** enable ntpdate  
Created symlink from /etc/systemd/system/multi-user.target.wants/ntpdate.service to /usr/lib/systemd/system/ntpdate.service.

国内常用的一些ntpserver^[[国内NTP Server](https://www.citydog.me/1352.html)]：

> 1.cn.pool.ntp.org   
2.cn.pool.ntp.org   
3.cn.pool.ntp.org   
0.cn.pool.ntp.org   
cn.pool.ntp.org   
tw.pool.ntp.org   
0.tw.pool.ntp.org   
1.tw.pool.ntp.org    
2.tw.pool.ntp.org    
3.tw.pool.ntp.org  

**设置history命令**  

> <font color='blue'>[root@hoster ~]#</font> **export** HISTTIMEFORMAT="%F %T "  
<font color='blue'>[root@hoster ~]#</font> vim ~/.bashrc  
#增加这行：export HISTTIMEFORMAT="%F %T "
  

**Ctrl + R搜索历史命令**  

在命令行提示符下按下Ctrl+R，终端将显示提示reverse-i-search。  
只要用关键字搜索一下历史命令然后重新执行这条命令而不需要将整条命令再输入一遍。


**下载文件wget命令^[[Centos下载文件wget命令详解](http://www.souvc.com/?p=1569)]**  

> <font color='blue'>[root@hoster ~]#</font> **wget** --spider http://mirrors.aliyun.com/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-1804.iso  
Spider mode enabled. Check if remote file exists.  
--2018-08-01 18:30:53--  http://mirrors.aliyun.com/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-1804.iso  
Resolving mirrors.aliyun.com (mirrors.aliyun.com)... 182.242.142.95, 182.242.142.87, 182.242.142.88, ...  
Connecting to mirrors.aliyun.com (mirrors.aliyun.com)|182.242.142.95|:80... connected.
HTTP request sent, awaiting response... 200 OK  
Length: 4470079488 (4.2G) [application/octet-stream]  
Remote file exists.  



### KVM虚拟化

#### 安装KVM^[[refer](https://www.server-world.info/en/note?os=CentOS_7&p=kvm&f=1)]  

[1]	Install KVM.  
> <font color='blue'>[root@hoster ~]#</font> **yum** -y install qemu-kvm libvirt virt-install bridge-utils  
<font color='grey'> # 确认kvm的模块加载了 </font>  
> <font color='blue'>[root@hoster ~]#</font>  **lsmod | grep kvm**   
kvm_intel             178927  0  
kvm                   578558  1 kvm_intel  
irqbypass              13503  1 kvm    
<font color='blue'>[root@hoster ~]#</font> **systemctl start libvirtd**    
<font color='blue'>[root@hoster ~]#</font> **systemctl enable libvirtd**    

[2]	配置KVM虚拟机网络，将原来通过物理网卡连接改为使用桥接网络连接。

> <font color='grey'>/*add bridge "br0"*/</font>    
[root@dlp ~]# nmcli c add type bridge autoconnect yes con-name br0 ifname br0   
Connection 'br0' (0f4b7bc8-8c7a-461a-bff1-d516b941a6ec) successfully added.  
 <font color='grey'>set IP for br0</font>    
[root@dlp ~]# nmcli c modify br0 ipv4.addresses 10.1.23.100/24 ipv4.method manual   
 <font color='grey'>set Gateway for br0</font>    
[root@dlp ~]# nmcli c modify br0 ipv4.gateway 10.1.23.254   
 <font color='grey'>set DNS for "br0"</font>    
[root@dlp ~]# nmcli c modify br0 ipv4.dns 61.139.2.69   
 <font color='grey'>remove the current setting，注意下面这步执行后，远程ssh的session会断开</font>    
[root@dlp ~]# nmcli c delete em2   
 <font color='grey'>add an interface again as a member of br0</font>    
[root@dlp ~]# nmcli c add type bridge-slave autoconnect yes con-name em2 ifname em2 master br0  
 <font color='grey'>重启操作系统使设置生效</font>  
[root@dlp ~]# reboot  
[root@dlp ~]# ip addr   
*1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000  
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00  
    inet 127.0.0.1/8 scope host lo  
       valid_lft forever preferred_lft forever  
    inet6 ::1/128 scope host  
       valid_lft forever preferred_lft forever  
2: em1: <BROADCAST,MULTICAST> mtu 1500 qdisc mq state DOWN group default qlen 1000  
    link/ether f0:1f:af:dc:28:0a brd ff:ff:ff:ff:ff:ff  
3: em2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq master br0 state UP group default qlen 1000  
    link/ether f0:1f:af:dc:28:0b brd ff:ff:ff:ff:ff:ff  
5: virbr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default qlen 1000  
    link/ether 52:54:00:cc:a7:56 brd ff:ff:ff:ff:ff:ff  
    inet 192.168.122.1/24 brd 192.168.122.255 scope global virbr0  
       valid_lft forever preferred_lft forever  
6: virbr0-nic: <BROADCAST,MULTICAST> mtu 1500 qdisc pfifo_fast master virbr0 state DOWN group default qlen 1000  
    link/ether 52:54:00:cc:a7:56 brd ff:ff:ff:ff:ff:ff  
7: br0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000  
    link/ether f0:1f:af:dc:28:0b brd ff:ff:ff:ff:ff:ff  
    inet 10.1.23.100/24 brd 10.1.23.255 scope global noprefixroute br0  
       valid_lft forever preferred_lft forever  
    inet6 fe80::bdd6:3601:9ab2:405d/64 scope link noprefixroute  
       valid_lft forever preferred_lft forever*  

#### 创建一台虚拟机^[[Create Virtual Machine#1](https://www.server-world.info/en/note?os=CentOS_7&p=kvm&f=2)]  








## 有用的链接 ##

[Server-world](https://www.server-world.info/en/)
