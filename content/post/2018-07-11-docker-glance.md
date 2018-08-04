---
title: Docker glance
author: ''
date: '2018-07-11'
slug: docker-glance
categories: []
tags: [docker]
---

*README^[此文是《Docker — 从入门到实践》一书的重点摘要。[Docker — 从入门到实践](https://yeasy.gitbooks.io/docker_practice/)]


1.Docker是“操作系统层面的虚拟化技术”^[[维基百科词条](https://zh.wikipedia.org/wiki/%E4%BD%9C%E6%A5%AD%E7%B3%BB%E7%B5%B1%E5%B1%A4%E8%99%9B%E6%93%AC%E5%8C%96)]

  >  操作系统层虚拟化（英语：Operating system–level virtualization），亦称容器化（英语：Containerization），是一种虚拟化技术，这种技术将操作系统内核虚拟化，可以允许用户空间软件实例（instances）被分区成几个独立的单元，在内核中运行，而不是只有一个单一实例运行。这个软件实例，也被称为是一个容器（containers），虚拟引擎（Virtualization engine），虚拟专用服务器（virtual private servers）或是 jails。对每个进程的拥有者与用户来说，他们使用的服务器程序，看起来就像是自己专用的。  


2.比传统VM更轻便、快捷  
　　对“文件系统、网络互联到进程”进行隔离，由于不同于传统VM需要虚拟硬件，因而比VM更轻便、快捷。 

3.Docker的三个基本概念

  - 镜像（Image）  
  - 容器（Container）  
  - 仓库（Repository）  

  > 镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的 类 和 实例 一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。  

　　Docker Registry是集中的存储、分发镜像的服务。最常使用的 Registry 公开服务是官方的 Docker Hub，这也是默认的Registry，并拥有大量的高质量的官方镜像。
　　
　　
　　
  
      
      