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



### 规范数据模型的三个层次^[规范数据模型（Canonical Data Model）的三层次图示——>[link](http://www.databaseanswers.org/data_models/canonical_data_models/index.htm)]###

1.反映事件序列的**概念数据模型**（Conceptual Data Model with Event Sequences）  
2.展示属性的**逻辑数据模型**（Logical Data Model showing Attributes）   
3.展示属性和数据类型的**物理数据模型**（Logical Data Model showing Attributes）  


### Dimensional Model(维度模型) ^[What is Dimensional Model in Data Warehouse? [link](https://www.guru99.com/dimensional-model-data-warehouse.html)]###
   
- 专为查询和数据仓库工具而优化的模型。  
- 由“事实表”（Fact Table）和“维度表”（dimension tables）组成。  
- [Dimensional modeling @Wikipedia](https://en.wikipedia.org/wiki/Dimensional_modeling)

![img](https://raw.githubusercontent.com/dean33/exblog/master/static/2018-07-19-data-warehosing-practice.files/Dimensional-Model.png)


### Operational Data Source (ODS) ###

- 设计目的：为运营报表、控制和决策提供支持。  
- 数据来源：一般来自多个生产系统。  
- 数据去向：一般传给数据仓库。  
- 与DW区别：DW一般是用来为经营战略战术提供决策支持，ODS支持的是日常经营/运营层面。  


> An operational data store (or "ODS") is a database designed to integrate data from multiple sources for additional operations on the data, for reporting, controls and operational decision support. Unlike a production master data store, the data is not passed back to operational systems. It may be passed for further operations and to the data warehouse for reporting.^[From Wikipedia [ODS](https://en.wikipedia.org/wiki/Operational_data_store)]




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



## 案例及经验  ##


[金融行业数据中心及数据仓库规划](http://www.oracle.com/technetwork/cn/community/developer-day/2-financial-industry-data-plan-1533690-zhs.pdf),By Oracle.

[银行数据仓库应用解决方案建议 ](https://wenku.baidu.com/view/6c0b80a07f1922791688e88f.html?sxts=1531980739308), By IBM 数据仓库服务部，2012.

[南昌商业银行数据仓库交流](https://wenku.baidu.com/view/da67750583d049649b6658f3.html),By 天正智能.

[恒丰银行——基于大数据技术的数据仓库应用建设](http://www.datayuan.cn/article/11424.htm),By 恒丰银行，2017.   

> Source: [*数据猿*](http://www.datayuan.cn)

[话说银行数据仓库的概论](http://www.solgle.com/news/375.html)，By Unkown,2017.







