---
title: Data Warehosing practice
author: ''
date: '2018-07-19'
slug: data-warehosing-practice
categories:
  - tech
tags: []
---

## 概念Concept  ##

### 第一范式、第二范式及第三范式^[Third-Normal Form (‘3NF’) Data Model 例子——>[link](https://blog.csdn.net/sunzhenhua0608/article/details/16850053)]  


>  **第一范式**  
[定义] 如果关系R 中所有属性的值域都是单纯域，那么关系模式R是第一范式的。  
那么符合第一模式的特点就有  
1)有主关键字  
2)主键不能为空  
3)主键不能重复  
4)字段不可以再分  
**第二范式**  
第二范式的主要任务就是满足第一范式的前提下，消除部分函数依赖（针对联合主键而言）。  
[定义]如果关系模式R是第一范式的，而且关系中每一个非主属性不部分依赖于主键，称R是第二范式的。  
**第三范式**  
在第二范式的基础上，不存在非主属性对主键的传递性依赖以及部分性依赖。


### 列式存储 ###

[相对于OLTP，列式存储到底好用在哪里？](http://dbaplus.cn/news-159-2032-1.html)



### 规范数据模型的三个层次^[规范数据模型（Canonical Data Model）的三层次图示——>[link](http://www.databaseanswers.org/data_models/canonical_data_models/index.htm)]###

1.反映事件序列的**概念数据模型**（Conceptual Data Model with Event Sequences）  
2.展示属性的**逻辑数据模型**（Logical Data Model showing Attributes）   
3.展示属性和数据类型的**物理数据模型**（Logical Data Model showing Attributes）  


### Dimensional Model(多维模型) ^[What is Dimensional Model in Data Warehouse? [link](https://www.guru99.com/dimensional-model-data-warehouse.html)]###
   
- 专为查询和数据仓库工具而优化的模型。  
- 由“事实表”（Fact Table）和“维度表”（dimension tables）组成。  
  - 事实表是用来记录具体事件的，包含了每个事件的具体要素，以及具体发生的事情；    
  - 维表则是对事实表中事件的要素的描述信息。  
- [Dimensional modeling @Wikipedia](https://en.wikipedia.org/wiki/Dimensional_modeling)

![img](https://raw.githubusercontent.com/dean33/exblog/master/static/2018-07-19-data-warehosing-practice.files/Dimensional-Model.png)

　　多维数据模型是为了满足用户从多角度多层次进行数据查询和分析的需要而建立起来的基于事实和维的数据库模型，其基本的应用是为了实现OLAP（Online Analytical Processing）。^[数据仓库的多维数据模型,[link](http://webdataanalysis.net/web-data-warehouse/multidimensional-data-model/)]
　　
　　
　　- 优点：基于分析优化的数据组织和存储模式。  
　　- 缺点：与关系模型相比其灵活性不够，一旦模型构建就很难进行更改。  




### Operational Data Source (ODS) ###

- 设计目的：为运营报表、控制和决策提供支持。  
- 数据来源：一般来自多个生产系统。  
- 数据去向：一般传给数据仓库。  
- 与DW区别：DW一般是用来为经营战略战术提供决策支持，ODS支持的是日常经营/运营层面。  


> An operational data store (or "ODS") is a database designed to integrate data from multiple sources for additional operations on the data, for reporting, controls and operational decision support. Unlike a production master data store, the data is not passed back to operational systems. It may be passed for further operations and to the data warehouse for reporting.^[From Wikipedia [ODS](https://en.wikipedia.org/wiki/Operational_data_store)]


### 元数据（Meta Data）^[数据仓库元数据管理[link](http://webdataanalysis.net/web-data-warehouse/meta-data/)] ###

元数据其实就是对数据的解释和描述，这种解释可以以多种形式存在，数据库的数据字典、外部文档，工具的资料档案库（Repository）等。

数据仓库的元数据分为3类：  
- 数据库管理系统的数据字典  
- ETL处理流程产生的日志  
- BI建模和分析中工具或文档中记录的信息  




### OLTP vs OLAP ###

**OLAP的基本操作^[数据立方体与OLAP,[link](http://webdataanalysis.net/web-data-warehouse/data-cube-and-olap/)]**  
OLAP的多维分析操作包括：钻取（Drill-down）、上卷（Roll-up）、切片（Slice）、切块（Dice）以及旋转（Pivot），下面还是以上面的数据立方体为例来逐一解释下：  

![img](https://raw.githubusercontent.com/dean33/exblog/master/static/2018-07-19-data-warehosing-practice.files/2018-07-20-OLAP-operation.png)

- **钻取（Drill-down）**：在维的不同层次间的变化，从上层降到下一层，或者说是将汇总数据拆分到更细节的数据，比如通过对2010年第二季度的总销售数据进行钻取来查看2010年第二季度4、5、6每个月的消费数据，如上图；当然也可以钻取浙江省来查看杭州市、宁波市、温州市……这些城市的销售数据。  
- **上卷（Roll-up）**：钻取的逆操作，即从细粒度数据向高层的聚合，如将江苏省、上海市和浙江省的销售数据进行汇总来查看江浙沪地区的销售数据，如上图。  
- **切片（Slice）**：选择维中特定的值进行分析，比如只选择电子产品的销售数据，或者2010年第二季度的数据。  
- **切块（Dice）**：选择维中特定区间的数据或者某批特定值进行分析，比如选择2010年第一季度到2010年第二季度的销售数据，或者是电子产品和日用品的销售数据。  
- **旋转（Pivot）**：即维的位置的互换，就像是二维表的行列转换，如图中通过旋转实现产品维和地域维的互换。  




**比较**  
- 联机事务处理On-Line Transaction Processing    
- 联机分析处理On-Line Analytical Processing

联机分析处理 (OLAP) 的概念最早是由关系数据库之父E.F.Codd于1993年提出的，他同时提出了关于OLAP的12条准则。OLAP的提出引起了很大的反响，OLAP作为一类产品同联机事务处理 (OLTP) 明显区分开来。

当今的数据处理大致可以分成两大类：联机事务处理OLTP（on-line transaction processing）、联机分析处理OLAP（On-Line Analytical Processing）。

OLTP是传统的关系型数据库的主要应用，主要是基本的、日常的事务处理，例如银行交易。OLAP是数据仓库系统的主要应用，支持复杂的分析操作，侧重决策支持，并且提供直观易懂的查询结果。

下表列出了OLTP与OLAP之间的比较。

|           | OLTP                             |   OLAP                |
| ----------|:--------------------------------:| ---------------------:|
| 用户      | 操作人员,低层管理人员            | 决策人员,高级管理人员 |
| 功能      | 日常操作处理                     | 分析决策              |
| DB设计    | 面向应用                         | 面向主题              |
| 数据      | 当前的, 最新的细节的,二维的分立的| 历史的, 聚集的, 多维的集成的, 统一的 |
| 数据模型  | 关系模型                         | 多维模型              |
| 存储      | 读/写数十条记录                  | 读上百万条记录        |
| 工作单位  | 简单的事务                       | 复杂的查询            |
| 用户数    | 上千个                           | 上百个                |
| DB大小    | 100MB-GB                         |  100GB-TB             |



![img](https://raw.githubusercontent.com/dean33/exblog/master/static/2018-07-19-data-warehosing-practice.files/2018-07-20-OLTP-vs-OLAP.png)



### 数据仓库不是一个产品 ###

一般说来是：  

- 平台产品  
  - 数据库  
  - 服务器  
  - 存储  
- 数据处理工具  
  - ETL工具  
  - 数据质量及数据管理工具  
- 前端应用工具  
  - OLAP工具  
  - 数据挖掘工具  
  - 报表及展现工具  
  - 门户等  
- 业务应用  
  - 自主开发（如报表、绩效考核等）  
  - 套装软件  
- 备份设备  




### 数据仓库特征及价值 ^[[数据仓库的价值](http://webdataanalysis.net/web-data-warehouse/value-of-data-warehouse/)]###

- 4个基本特征：  
  - 面向主题的  
  - 集成的  
  - 相对稳定的  
  - 记录历史的  

- 4个价值：  
  - 高效的数据组织形式  
  - 时间价值  
  - 集成价值  
  - 历史数据    


## 游戏行业的实践  ##




## 案例及经验  ##



[金融行业数据中心及数据仓库规划](http://www.oracle.com/technetwork/cn/community/developer-day/2-financial-industry-data-plan-1533690-zhs.pdf),By Oracle.

[银行数据仓库应用解决方案建议 ](https://wenku.baidu.com/view/6c0b80a07f1922791688e88f.html?sxts=1531980739308), By IBM 数据仓库服务部，2012.

[南昌商业银行数据仓库交流](https://wenku.baidu.com/view/da67750583d049649b6658f3.html),By 天正智能.

[恒丰银行——基于大数据技术的数据仓库应用建设](http://www.datayuan.cn/article/11424.htm),By 恒丰银行，2017.   



[话说银行数据仓库的概论](http://www.solgle.com/news/375.html)，By Unkown,2017.

[360数据处理平台的架构演进及优化实践](http://dbaplus.cn/news-73-2124-1.html), By 360大数据开发经理-王素梅, 2018.07

[中小型企业大数据体系建设的核心技术选型](http://dbaplus.cn/news-73-2046-1.html),By Tumweeg,2018-05


## 技术选型  ##

### 初选 ###

[Apache Kylin](http://kylin.apache.org/cn/),(Extreme OLAP Engine for Big Data,基于Hadoop的开源数据仓库OLAP分析引擎) 

开源MySQL数据仓库解决方案：Infobright. ^[[开源MySQL数据仓库解决方案：Infobright](https://www.biaodianfu.com/mysql-infobright.html)]

[数据仓库方案选型](https://blog.csdn.net/zzq900503/article/details/78465369)

[聊聊Greenplum的那些事](https://blog.csdn.net/paicmis/article/details/53576859)

[数据仓库简介](https://www.slideshare.net/vnnw/bi-8180370)，2011.6

[阿里云大数据三次技术突围：Greenplum、Hadoop和飞天](http://www.voidcn.com/article/p-szfepnat-bqs.html),2017.11

### Pivotal Greenplum ###


- [Pivotal践行见远技术篇之(14) -跟您聊聊Greenplum的那些事儿 (上)](https://mp.weixin.qq.com/s/TiH-fRdy0QnOifOA-5MfXw)  
- [Pivotal践行见远技术篇之(14) -跟您聊聊Greenplum的那些事儿 (下)
](https://mp.weixin.qq.com/s/6KMtKYQib7H-XsWsAAuA_g)   
- [【干货】数字化转型时代的数据仓库（一）](https://mp.weixin.qq.com/s/MFyEnuJqX-GNgJRqLqvBGQ)  
- [【干货】数字化转型时代的数据仓库（二）](https://mp.weixin.qq.com/s/xY-MoSgc8PfOtTs4pUqaCw)  
- [Greenplum在企业生产中的最佳实践](https://mp.weixin.qq.com/s/mG_EqxS5l1J_jdVJM2spQQ)  
- [Greenlum在企业生产中的案例实践 (下）](https://mp.weixin.qq.com/s/LKQPuNmmU92chSXTUpvrtA)  
- [Pivotal Greenplum 5.3 特性简介](https://mp.weixin.qq.com/s/i87U8kSxgz1jBqLusnV_0w)  
- [GemFire与Greenplum的最佳集成实践之实施经验谈](https://mp.weixin.qq.com/s/KN-59TdCpY-KpKYjv580Fg)  
- [【视频和PPT分享】如何通过技术方式消除Kubernetes痛点](https://mp.weixin.qq.com/s/HmZ2mqRDQyJAVpRNEA5sAA)  
- [Adaptability-as-a-Service with Kubernetes](https://mp.weixin.qq.com/s/kmZORCEaN50j-pmR01zd0A)  
- [事件驱动型架构，究竟要怎样构建？](https://mp.weixin.qq.com/s/d60NwWumlrUAubWoPTvmnw)  


## 有用的信息源  ##

>  [数据猿](http://www.datayuan.cn)  
   [网站数据分析](http://webdataanalysis.net/)  
   [Pivotal微信] 微信号：pivotal_china
   


