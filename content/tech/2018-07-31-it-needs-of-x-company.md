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
- 虚拟化：KVM    
- 邮件系统：Mail  
- 文档协作：Git  
- 目录管理：LDAP  
- *开发管理：持续集成与部署CI/CD*  
- *运行监测：Zabbix*  
- ERP：[odoo](http://www.odoo.com)或其他开源ERP^[[值得考虑的九大开源ERP系统](http://os.51cto.com/art/201804/570668.htm)]  
  
  
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


**查看是否安装了某软件**  


>[root@djwy-153 ~]#  **yum list installed | grep mysql**  
Repodata is over 2 weeks old. Install yum-cron? Or run: yum makecache fast  
mysql-community-client.x86_64       5.7.20-1.el7                       @mysql57-community  
mysql-community-common.x86_64       5.7.20-1.el7                       @mysql57-community  
mysql-community-libs.x86_64         5.7.20-1.el7                       @mysql57-community  
mysql-community-libs-compat.x86_64  5.7.20-1.el7                       @mysql57-community  
mysql-community-server.x86_64       5.7.20-1.el7                       @mysql57-community  
mysql57-community-release.noarch    el7-8                              installed  
php-mysql.x86_64                    5.4.16-43.el7_4                    @updates  



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

**修改主机名^[[如何在CentOS 7上修改主机名](https://www.jianshu.com/p/39d7000dfa47)]**  

> <font color='blue'>[root@hoster ~]#</font> **hostnamectl** set-hostname test  
<font color='blue'>[root@hoster ~]#</font> vim /etc/hosts  
#127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4  
127.0.0.1   test  
#::1         localhost localhost.localdomain localhost6 localhost6.localdomain6  
::1        test  

然后reboot重启即可。



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

**查看用户登录日志**

１、命令

**w或who**  

  >查看当前登入系统的用户信息。其中who -m等效于who am i。
  
**lastlog**

>列出所有用户最近登录的信息，或者指定用户的最近登录信息。lastlog引用的是/var/log/lastlog文件中的信息，包括login-name、port、last login time　　

**last**

>列出当前和曾经登入系统的用户信息，它默认读取的是/var/log/wtmp文件的信息。输出的内容包括：用户名、终端位置、登录源信息、开始时间、结束时间、持续时间。


２、文件
Linux用户登录信息放在三个文件中：

/var/run/utmp：记录当前正在登录系统的用户信息，默认由who和w记录当前登录用户的信息，uptime记录系统启动时间；

/var/log/wtmp：记录当前正在登录和历史登录系统的用户信息，默认由last命令查看；　　

/var/log/btmp：记录失败的登录尝试信息，默认由lastb命令查看。　　

这三个文件都是二进制数据文件，并且三个文件结构完全相同,是由/usr/include/bits/utmp.h文件定义了这三个文件的结构体。



**下载文件wget命令^[[Centos下载文件wget命令详解](http://www.souvc.com/?p=1569)]**  

> <font color='blue'>[root@hoster ~]#</font> **wget** - -spider http://mirrors.aliyun.com/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-1804.iso  
Spider mode enabled. Check if remote file exists.  
--2018-08-01 18:30:53--  http://mirrors.aliyun.com/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-1804.iso  
Resolving mirrors.aliyun.com (mirrors.aliyun.com)... 182.242.142.95, 182.242.142.87, 182.242.142.88, ...  
Connecting to mirrors.aliyun.com (mirrors.aliyun.com)|182.242.142.95|:80... connected.
HTTP request sent, awaiting response... 200 OK  
Length: 4470079488 (4.2G) [application/octet-stream]  
Remote file exists.  

**查看指定目录所占容量大小**

>[root@boss420 zjdl]# **du -h --max-depth=1**  
104K    ./arts  
88M     ./design  
5.0G    ./client  
5.1G    .  

>[root@boss420 zjdl]# **du -h --max-depth=0**  
5.1G    .

**修改ls目录看不清的黑底篮字体^[[Linux文本界面字体颜色修改](https://blog.csdn.net/zonghua521/article/details/78197976)]**

在文本界面 系统目录的字体颜色是 黑底蓝字  严重看不清楚，对此作出修改

使用 vi 编辑进入  /etc/DIR_COLORS

找到“DIR 01;34   # directory”，将34改为36


数字代表的颜色 在下面会有显示,你可以找到文件的两行注释：
//Text color codes:  
//30=black 31=red 32=green 33=yellow 34=blue 35=magenta 36=cyan 37=white


**编辑.bashrc达到修改终端颜色效果**

参考：[PS1应用之——修改linux终端命令行各字体颜色](https://www.cnblogs.com/Q--T/p/5394993.html)

> [root@boss420 ~]# vim .bashrc

加入下面一行后保存退出:

>  PS1="\[\e[37;40m\][\[\e[32;40m\]\u\[\e[37;40m\]@\h \[\e[36;40m\]\w\[\e[0m\]]\\$ " 

重新加载bash配置文件即可生效:

> [root@boss420 ~]# source .bashrc


**修改vim中字体颜色**

1. vim ~/.vimrc 加入如下内容，将注释字体设置白色并不加粗
 
> hi Comment ctermfg=white cterm =none 
  cterm若设置为bold就是粗体。

![img](https://raw.githubusercontent.com/dean33/exblog/master/static/2018-07-31-it-needs-for-company.files/2018-08-08-it-needs-vim-font-color.png)


**让所有用户显示行号** 

输入命令：vim /etc/vimrc

在vimrc文件的最后添加：set nu,保存：wq

手动加载配置：source /etc/bashrc

这样不管是哪个用户在vim下都显示行号






**修改IP地址**

1、设置网卡信息  

>[root@localhost network-scripts]# vi ifcfg-eth0  
NAME="eth0"  
HWADDR="52:54:00:5f:c1:ea"  
ONBOOT=yes  
NETBOOT=yes  
UUID="45e9e09e-fcce-4141-9b12-035c40898eca"  
IPV6INIT=yes  
BOOTPROTO=static  
TYPE=Ethernet  
**IPADDR=10.1.23.110  
NETMASK=255.255.255.0  
GATEWAY=10.1.23.254  
DNS=61.139.2.69**  

2、重启网络  

>[root@localhost network-scripts]# systemctl restart network.service

3、nameserver设置

>[root@vm1 ~]# ping www.baidu.com  
ping: www.baidu.com: Name or service not known

>[root@vm1 ~]# vi /etc/resolv.conf  
nameserver 8.8.8.8  
nameserver 8.8.4.4  


**网络故障排查步骤^[[Linux网络故障排查总结](https://blog.csdn.net/li_101357/article/details/70257001)]**  

1、检查网络设备  
网卡必须处在up状态（state必须处于up状态）

2、检查IP地址是否配置上了  

>[root@vm1 ~] ip addr

3、配置网关和路由  

查看路由：

>[root@boss420 ~]# ip route show  
default via 10.1.23.254 dev br0 proto static metric 425  
10.1.23.0/24 dev br0 proto kernel scope link src 10.1.23.100 metric 425  
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1  
192.168.122.0/24 dev virbr0 proto kernel scope link src 192.168.122.1  


4、检查域名解析

修改/etc/resolve.conf文件

5、写入/etc/network/interface下的网卡配置文件，否则重启后不生效。


**查看系统已启动的服务**  

>[root@boss420 ~]# systemctl list-units --type=service  


**任务管理器top**

[top linux下的任务管理器](http://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/top.html#top)

Top下的常用交互命令：  

> q：退出top命令  
<Space>：立即刷新  
s：设置刷新时间间隔  
c：显示命令完全模式  
t:：显示或隐藏进程和CPU状态信息  
m：显示或隐藏内存状态信息  
l：显示或隐藏uptime信息  
f：增加或减少进程显示标志  
S：累计模式，会把已完成或退出的子进程占用的CPU时间累计到父进程的MITE+  
P：按%CPU使用率排行  
T：按MITE+排行    
M：按%MEM排行  
u：指定显示用户进程  
r：修改进程renice值  
kkill：进程  
i：只显示正在运行的进程  
W：保存对top的设置到文件^/.toprc，下次启动将自动调用toprc文件的设置。  
h：帮助命令。  
q：退出  
注：强调一下，**使用频率最高的是P、T、M**，因为通常使用top，我们就想看看是哪些进程最耗cpu资源、占用的内存最多  

### crontab ###

1、增加配置： 

> [root@r420 /home/zdy/sync]# vim /etc/crontab

![img](https://raw.githubusercontent.com/dean33/exblog/master/static/2018-07-31-it-needs-for-company.files/2018-08-10-crontab.png)

2、检查当前crond服务是否启动

>[root@r420 ~]# **service crond status**  
Redirecting to /bin/systemctl status crond.service  
-crond.service - Command Scheduler  
   Loaded: loaded (/usr/lib/systemd/system/crond.service; enabled; vendor preset: enabled)  
   Active: active (running) since Fri 2018-08-03 13:36:27 CST; 1 weeks 0 days ago  
 Main PID: 1260 (crond)  
    Tasks: 1  
   Memory: 500.0K  
   CGroup: /system.slice/crond.service  
           └─1260 /usr/sbin/crond -n  
   ...



### Samba ###

**概念**

Unix Like 上面可以分享档案数据的 file system 是 NFS
Windows 上面使用的『网络上的芳邻』所使用的文件系统则称为 Common Internet File System, CIFS

SAMBA提供跨平台的文件访问服务^[[鸟哥：第十六章、文件服务器之二： SAMBA 服务器](http://cn.linux.vbird.org/linux_server/0370samba.php)]。

1、Server Message Block (SMB)  
2、SAMBA 则是透过两支服务来控制这两个步骤，分别是：

- nmbd ：这个 daemon 是用来管理工作组啦、NetBIOS name 啦等等的解析。主要利用 UDP 协议开启 port 137, 138 来负责名称解析的任务；  
- smbd ：这个 daemon 的主要功能就是用来管理 SAMBA 主机分享的目录、档案与打印机等等。 主要利用可靠的 TCP 协议来传输数据，开放的端口为 139 及 445(不一定存在) 。



**配置步骤^[[Limited Accessed Shared Folder](https://www.server-world.info/en/note?os=CentOS_7&p=samba&f=2)]**

1.创建待共享的目录，并给予适当权限  

2.创建samba访问账号
（1）创建操作系统账号

> [root@r420 /etc/samba]# **useradd project**  

（2）创建samba账号
> [root@r420 /etc/samba]# **pdbedit -a -u project**  


3.配置samba配置文件

> [root@r420 /home/zdy/sync]# vim /etc/samba/smb.conf

比较重要的有：

> [global]  
  unix charset = UTF-8  
  dos charset = CP932  
  hosts allow = 127.  10.1.  
  security = user  
  passdb backend = tdbsam  
  [project] *-----> 希望共享用户看到的目录名字，随便取*  
  path = /home/zdy/partner/zjdl  
  writable = yes  
  browsable = yes  
  create mode = 0770  
  directory mode = 0770  
  valid users = @project  *-----> 指定属于project组的linux用户才能访问*
  
配置修改之后重启服务：

> [root@r420 /home/zdy/partner/zjdl]# **systemctl restart smb nmb**
  
4.查看smb服务情况
  
  （1）smb.service服务：
  
> [root@r420 /home/zdy/partner/zjdl]# **systemctl status smb.service**  
- smb.service - Samba SMB Daemon  
   Loaded: loaded (/usr/lib/systemd/system/smb.service; enabled; vendor preset: disabled)  
   Active: active (running) since Fri 2018-08-10 13:23:53 CST; 1h 44min ago  
 Main PID: 29007 (smbd)  
   Status: "smbd: ready to serve connections..."  
    Tasks: 6  
   Memory: 6.3M  
   CGroup: /system.slice/smb.service  
           ├─29007 /usr/sbin/smbd --foreground --no-process-group  
           ├─29009 /usr/sbin/smbd --foreground --no-process-group  
           ├─29010 /usr/sbin/smbd --foreground --no-process-group  
           ├─29011 /usr/sbin/smbd --foreground --no-process-group  
           ├─29013 /usr/sbin/smbd --foreground --no-process-group  
           └─29042 /usr/sbin/smbd --foreground --no-process-group  

  （2）nmb.service服务：
  
>[root@r420 /home/zdy/partner/zjdl]# **systemctl status nmb.service**  
- nmb.service - Samba NMB Daemon  
   Loaded: loaded (/usr/lib/systemd/system/nmb.service; enabled; vendor preset: disabled)  
   Active: active (running) since Fri 2018-08-10 13:23:53 CST; 1h 45min ago  
 Main PID: 29005 (nmbd)  
   Status: "nmbd: ready to serve connections..."  
    Tasks: 1  
   Memory: 1.8M  
   CGroup: /system.slice/nmb.service  
           └─29005 /usr/sbin/nmbd --foreground --no-process-group  

  （3）排错可查看日志
  
> [root@r420 /home/zdy/partner/zjdl]# journalctl -xe
  

5、Window下访问

(1)打开命令行  

> \\10.1.23.100

(2)检查windows下保存的密码凭据,命令行下：

> control userpasswords2


  
**一个比较全的配置参考：[Samba](http://blog.mingguilu.com/2017/02/23/CentOS7%E4%BD%BF%E7%94%A8YUM%E6%90%AD%E5%BB%BASamba%E6%96%87%E4%BB%B6%E5%85%B1%E4%BA%AB/)**


### KVM虚拟化

> [root@boss420 ~]# yum install vnc-server tigervnc -y  

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

1、执行下面的命令  
> 
<font color='blue'>[root@hoster ~]#</font> virt-install \  
--name test \  
--ram 4096 \  
--disk path=/var/kvm/images/test.img,size=30 \  
--vcpus 2 \  
--os-type linux \  
--os-variant rhel7 \  
--network bridge=br0 \  
--graphics none \  
--console pty,target_type=serial \  
--location 'http://mirrors.aliyun.com/centos/7/os/x86_64/' \  
--extra-args 'console=ttyS0,115200n8 serial'  

2、进入文字模式安装  

3、宿主机、客户机的切换  
进入客户机：

> [root@boss420 qemu]# **virsh** console test  
Connected to domain test  
Escape character is ^]  

退出客户机回到宿主机：
按热键：ctrl+]


4、克隆这个干净的虚拟机硬件文件为模板以后备用  

> [root@boss420 qemu]# **virt-clone** --original test --name template --file /var/kvm/images/template.img  
Allocating 'template.img'              |  30 GB  00:00:13
Clone 'template' created successfully.

>[root@boss420 images]# virt-clone -o template -n vm1 -f /var/kvm/images/vm1.img


5、安装有用的virt管理工具^[[Virt-Tools](https://www.server-world.info/en/note?os=CentOS_7&p=kvm&f=9)]

> [root@boss420 qemu]# yum -y install libguestfs-tools virt-top



删除虚拟机^[[虚拟化之KVM virsh常用命令篇](http://www.cnblogs.com/lin1/p/5776280.html)]  

>[root@boss420 images]# **virsh** destroy centos7  
Domain centos7 destroyed  
[root@boss420 images]# **virsh** undefine centos7  
Domain centos7 has been undefined  


#### 直接从模板创建新的虚拟机（克隆）

1、virt-clone 克隆  

> [root@boss420 images]# virt-clone -o template -n vm1 -f /var/kvm/images/vm1.img  
template  //备好的模板映像文件  
vm1       //新的虚拟机名称  
vm1.img   //新虚拟机文件的映像文件  

2、在hoster宿主机上找到新虚拟机的网卡地址，并记录   

> [root@boss420 images]# cat /etc/libvirt/qemu/vm1.xml   
找到mac地址：**mac address='52:54:00:68:52:de'**  

3、启动新虚拟机  

> [root@boss420 images]# virsh start vm1  

4、在虚拟机中修改网卡地址、配置IP地址  

> [root@localhost ~]# cd /etc/sysconfig/network-scripts   
[root@localhost network-scripts]#ip addr			#得到虚拟机eth接口名称  
[root@localhost network-scripts]# mv ifcfg-eth0 ifcfg-ethx    #目标名称与上一步中得到的保持一致  
[root@localhost network-scripts]# vi ifcfg-ethx  
修改mac，用上面找到的mac地址  
HWADDR="52:54:00:83:68:11"  
IPADDR=10.1.23.111    
NETMASK=255.255.255.0    
GATEWAY=10.1.23.254    
DNS=61.139.2.69    




5、修改hostname，并reboot重启生效。  

### 设置虚拟机开机自动启动 ###  


> [root@boss420 ~]# **virsh autostart** test    
Domain test marked as autostarted  
[root@boss420 ~]# cd /etc/libvirt/qemu/autostart/  
[root@boss420 autostart]# ll  
total 0  
lrwxrwxrwx 1 root root 26 Aug  3 20:09 test.xml -> /etc/libvirt/qemu/test.xml  
[root@boss420 autostart]# **virsh autostart** vm1  
Domain vm1 marked as autostarted  
[root@boss420 autostart]# **virsh autostart** vm2  
Domain vm2 marked as autostarted  




### 解决虚拟机无法ping通网关的问题 ###

1、在host上，查看虚拟机的网卡接口是否加载到网桥br0  

> [root@boss420 ~]# **brctl show**  
bridge name     bridge id               STP enabled     interfaces  
br0             8000.f01fafdc280b       yes             em2  
docker0         8000.02421b137ce4       no              veth19e8cd2  
virbr0          8000.525400cca756       yes             virbr0-nic  

发现第一行的br0的interfaces字段，只有host自身的em2网卡，没有虚拟机的网卡，需要添加。

2、增加test、vm1、vm2三台虚拟机的interface到br0  

> [root@boss420 ~]# brctl addif br0 vnet0  
[root@boss420 ~]# brctl addif br0 vnet1  
[root@boss420 ~]# brctl addif br0 vnet2  



[在 CentOS 7 中所不見的命令](https://shazi.info/%E5%9C%A8-centos-7-%E4%B8%AD%E6%89%80%E4%B8%8D%E8%A6%8B%E7%9A%84%E5%91%BD%E4%BB%A4-round-1%EF%BC%9A-ifconfig%E3%80%81route%E3%80%81netstat%E3%80%81traceroute/)


## DOCKER ##

See this [article](/note/2018/08/03/docker-study/)






## 有用的链接 ##

[Server-world](https://www.server-world.info/en/)

[极客学院Linux Wiki](http://wiki.jikexueyuan.com/list/linux/)
