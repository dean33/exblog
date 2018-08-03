---
title: Docker study
author: ''
date: '2018-08-03'
slug: docker-study
categories: []
tags: []
---

## 概念 ##


1、什么是docker 

Docker是一个开放源代码软件项目，让应用程序布署在软件容器下的工作可以自动化进行，借此在Linux操作系统上，提供一个额外的软件抽象层，以及操作系统层虚拟化的自动管理机制^[[wiki的定义](https://zh.wikipedia.org/wiki/Docker_(%E8%BB%9F%E9%AB%94)#cite_note-SYS-CON_Media-1)]



2、什么是容器平台（CONTAINER PLATFORM）？

能够为CIO或架构师在管理应用或架构的整个生命周期过程中提供便利。包括：security, governance, automation, support and certification。


3、案例

实践docker从现有开始，使应用更快、更安全、成本更低、更易于管控。

- MODERNIZE TRADITIONAL APPS [MTA]  
- HYBRID CLOUD  
- CONTINUOUS INTEGRATION AND DEPLOYMENT [DEVOPS]  [WHITE PAPER - DOCKER AND DEVOPS](https://www.docker.com/sites/default/files/WP_Docker%20and%20the%203%20ways%20devops.pdf)  
- MICROSERVICES  



## 操作 ##

1、查看已有的docker的镜像——**docker images**  

>[root@boss420 ~]# docker images  
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE  
my_image/centos_httpd   latest              da6cbf04e210        22 hours ago        361 MB  
docker.io/centos        latest              49f7960eb7e4        8 weeks ago         200 MB  


2、进入指定docker的bash命令行——**docker run**    

>[root@boss420 ~]# docker run -it -p 8081:80 my_image/centos_httpd /bin/bash  
[root@797fa3ef5f33 /]

3、退出docker到宿主机——**连续按Ctrl+p, Ctrl+q**


4、查看运行中的docker——**docker ps**

>[root@boss420 ~]# docker ps  
CONTAINER ID        IMAGE                   COMMAND             CREATED             STATUS              PORTS                  NAMES  
797fa3ef5f33        my_image/centos_httpd   "/bin/bash"         9 minutes ago       Up 9 minutes        0.0.0.0:8081->80/tcp   vibrant_pasteur  


5、重新进入docker——**docker attach**

>[root@boss420 ~]# docker attach 797fa3ef5f33  
[root@797fa3ef5f33 html]#
