# Tomcat

## 目录介绍

bin					专门用来存放tomcat服务器的可执行程序

conf				  专门用来存放tomcat的配置文件

lib					  专门用来存放tomcat服务器jar包

logs				   专门用来存放tomcat服务器运行时输出的日志信息

temp				 专门用来存放tomcat运行时产生的临时数据

webapps		  专门用来存放部署的web工程

work				 是tomcat工作时的目录，可以存放tomcat运行时jsp翻译为servlet源码，和session钝化的目录

## 启动

1. bin目录下startup.bat

2. 命令行，进入tomcat的bin目录下，数据catalina run，这种方法可以看到错误信息

## 修改tomcat端口号

默认端口号：8080

找到tomcat目录下的conf目录，找到server.xml配置文件

找到Connector标签，修改port属性，端口号:1-65535，尽量不要是1000以内的，重启Tomcat服务器

## 部署web工程到Tomcat中

方式一：只需要把web工程的目录拷贝到Tomcat的webapps目录下即可

方式二：找到Tomcat下的conf目录\catalina\localhost下，创建如下的配置文件

~~~xml
<!-- Context表示一个工程上下文 
	path表示工程的访问路径：/abc
	docBase：表示你的工程目录在哪里
-->

<Context path="/abc" docBase="I:\Develop\book" />
~~~

http://localhost:8080/abc/index.html

**[linux配置jdk](https://www.cnblogs.com/fanqisoft/p/11975562.html)**

**[ubuntu开放指定端口](https://www.jianshu.com/p/2ec5d16db02b)**

## WebApps下的ROOT

是默认访问工程

http://ip:port			没有工程名，默认访问webapps下的index.jsp

http://IP:prot/工程名/	没有资源名，默认访问index.html