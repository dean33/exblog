---
title: Develpment Environment Setup
author: ''
date: '2018-08-08'
slug: develpment-environment-setup
categories: [tech]
tags: []
---


### Java环境 ###

1、下载jdk安装

2、配置环境变量

- 新增”Java_Home“：“C:\Program Files\Java\jdk1.8.0_181”   
- 编辑“path”：最前面加上：“%Java_Home%\bin;%Java_Home%\jre\bin;”  
- 新建“CLASSPATH”：
“%Java_Home%\bin;%Java_Home%\lib\dt.jar;%Java_Home%\lib\tools.jar”  

3、执行jar包中的一个类中的main方法

> C:\...\gs-maven\0.1.0>**java -cp gs-maven-0.1.0.jar main.java.hello.HelloWorld**  
Hello world!


### Eclipse 安装 ###


1、下载安装器[Dowload Eclipse](https://www.eclipse.org/downloads/)，并安装。更多参考^[[Eclispe安装](http://www.runoob.com/eclipse/eclipse-install.html)]

>47M的安装器：eclipse-inst-win64.exe  


2、字符集从默认的GBK改为UTF-8：[Eclipse 修改字符集](http://www.runoob.com/eclipse/eclipse-charset.html)





### Maven^[[Building Java Projects with Maven](https://spring.io/guides/gs/maven/)] ###

1、下载zip格式的含bin的文件：[maven](http://maven.apache.org/download.cgi)

> 8M的zip文件：apache-maven-3.5.4-bin.zip

2、解压至：E:\dev\apache-maven-3.5.4

3、设置环境变量

>(1)新建M2_HOME:"E:\dev\apache-maven-3.5.4"  
(2)编辑path：最后面加上“;%M2_HOME%\bin;”

4、控制台cmd检查是否成功

> mvn -v


**POM** stands for "**Project Object Model**". It is an XML representation of a Maven project held in a file named pom.xml.

5、编译

> E:\eclipse-workspace\HelloMaven>**mvn compile**  

会在项目的根目录下，生成target目录，放置class文件和jar文件。

>-HelloMaven  
　　-src  
　　-target  
　　　-classes  
　　　　-hello  
　　　　　-HelloWorld.class  
　　　　　-Greeter.class  
　　-gs-maven-0.1.0.jar  
    

6、打包

> E:\eclipse-workspace\HelloMaven>**mvn install**  

会将jar包发布到本地机器的maven repo目录下：

> C:\Users\zhangdy\.m2\repository\org\springframework\gs-maven\0.1.0

### SpringBoot ###

1、解决mvn install项目时报环境错：


> 环境：eclipse  
  报错：No compiler is provided in this environment. Perhaps you are running on a JRE rather than a JDK?  
  解决办法^[[参考](https://blog.csdn.net/yangtzh/article/details/45057273)]：需要将eclipse里默认的JRE地址，改为JDK的地址，因为mvn需要使用。  

Eclipse中的修改位置：在-->【Window】-->【Prefrences】-->【Java】-->【Installed JREs】

![img](https://raw.githubusercontent.com/dean33/exblog/master/static/2018-08-08-development-env.files/2018-08-08-development-env-mvn-eclipse-jre.png)

2、访问网页：http://localhost:8080/greeting

![img](https://raw.githubusercontent.com/dean33/exblog/master/static/2018-08-08-development-env.files/2018-08-08-development-env-springboot-run-default.png)

   访问网页带参数：http://localhost:8080/greeting?name=zdy

![img](https://raw.githubusercontent.com/dean33/exblog/master/static/2018-08-08-development-env.files/2018-08-08-development-env-springboot-run-edit-param.png)









