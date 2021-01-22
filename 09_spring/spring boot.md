# spring boot

## 1. Spring Boot简介

（1.1）描述：

spring boot微服务应用，官网：http://spring.io

spring boot不是对spring功能增强，它提供的是一种更快速的spring方式

（1.2）特点

- 创建独立的spring应用程序

- 嵌入了tomcat，无需部署war包

- 简化maven配置
- 自动配置spring
- 开箱即用，没有代码生成，无序xml配置

（1.3）spring的优缺点

- 优点：
  - 快速构建项目
  - 对矿建（主流框架：SSM）无配置集成
  - spring boot管理的项目是独立运行（无需依赖外部servlet容器）
  - 提供开发和部署的效率
  - 通常开发中spring boot会与云计算集成
- 缺点：
  - 帮助文档不全面
  - 作为架构设计，如果没有数据作为前提分析条件，使用spring boot有点多余

## 2. spring boot项目的构建

工程创建的四种方式：

- https://start.spring.io/
- sts构建spring boot项目（掌握）
- IDEA构建spring boot项目
- maven方式构建（pom文件添加spring boot相关依赖，需要开发者自己添加）

@RestController相当于@RequestBody和@Controller的组合，所有的数据都是以json的格式输出，不需要jackson的配置了