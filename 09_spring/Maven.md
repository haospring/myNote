# Maven

## maven的核心概念

1. pom.xml 项目对象模型。maven把一个项目当做一个模型使用。控制Maven构建项目的过程，管理jar依赖
2. 预定的目录结构：maven项目的目录和文件的位置都是规定的
3. 坐标：是一个唯一的字符串，用来表示资源的
4. 依赖管理：管理项目可以使用jar文件
5. 仓库管理（了解）：资源存放的位置
6. 生命周期（了解）：maven工具构建项目的过程
7. 插件和目标（了解）：执行maven构建的时候用的工具
8. 继承
9. 聚合

### pom

modelVersion：版本号

groupId：域名倒写

artifactId：项目名称，模块名称

version：项目的版本号

前三项称为坐标，用来唯一的标识项目

packaging：项目打包的类型，jar、war、rar、ear、pom，默认是jar，web应用是war，packaging可以不写

dependencies和dependence：依赖，项目中要使用的各种资源说明

properties：设置属性

build：maven在进行项目的构建时，配置信息，例如指定编译java代码使用的jdk的版本