### SSM整合

## CRUD

创建（create）

检索（retrieve）

更新（update）

删除（delete）

## 功能点

1. 分页

2. 数据校验

   jquery前端校验+jsr303后端校验

3. ajax

4. rest风格的URI；使用HTTP协议请求方式的，来表示对资源的操作（GET（查询），POST（新增），PUT（修改），DELETE（修改））

## 技术点

- 基础框架 - ssm

- 数据库 - mysql

- 前端框架 - bootstrap快速搭建简洁美观的界面

- 项目的依赖管理 - maven

- 分页插件 - pagehelper
- 逆向工程 - mybatis generator

## 基础环境搭建

- 创建maven工程
- maven配置文件配置

~~~xml
<!-- 配置阿里云的镜像仓库 -->
<mirror>
    <id>alimaven</id>
    <name>aliyun maven</name>
    <mirrorOf>central</mirrorOf>
    <url>https://maven.aliyun.com/repository/public</url>
</mirror>
~~~

~~~xml
<!-- 配置本地仓库位置 -->
<localRepository>I:/Develop/repository</localRepository>
~~~

- 引入依赖的jar包
  - spring
  - springmvc
  - mybatis
  - mysql
  - 连接池
  - 其他（jstl、javax.servlet-api、junit、jsp-api）
- 引入bootstrap前端框架
  - 先下载，然后参考官方文档
- 编写ssm整合的关键配置文件
  - web.xml
  - spring
  - springmvc
  - mybatis，使用mybatis的逆向工程生成对应的bean以及mapper