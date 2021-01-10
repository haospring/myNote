# Mybatis框架

## 1. 简介

## 1.1 什么是Mybatis

- MyBatis 是一款优秀的**持久层框架**
- 它支持自定义 SQL、存储过程以及高级映射
- MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作
- MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO为数据库中的记录。
- Mybatis本是apache的一个开源项目iBatis，2010年迁到Google code，并改名为Mybatis
- 2013年11月迁移到Github

### 1.2 持久层

数据持久化

- 持久化就是将程序的数据在持久状态和瞬时状态转化的过程
- 内存：断电即失
- 数据库（jdbc），io文件持久化

### 1.3 好处

- 传统的JDBC代码太复杂了，Mybatis可以减少开发人员的工作量
- 帮助程序员将数据存入到数据库中
- sql和代码分离，提高可维护性
- 提供映射标签，支持对象与数据库的ORM字段关系映射
- 提供对象关系映射标签，支持对象关系组建维护
- 提供xml标签，支持编写动态sql

## 2. 第一个Mybatis程序

搭建环境-->导入Mybatis-->编写代码-->测试

[官方文档](https://mybatis.org/mybatis-3/zh/getting-started.html)

### 2.1 搭建环境

搭建数据库

mybatis-config.xml

~~~xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <properties resource="jdbc.properties"/>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper resource="userMapper.xml"/>
    </mappers>
</configuration>
~~~

userMapper.xml

~~~xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!-- 绑定一个对应的dao/mapper接口 -->
<mapper namespace="com.haospring.dao.UserDao">
    <select id="getUser" resultType="com.haospring.pojo.User">
        select *
        from user;
    </select>
</mapper>
~~~

jdbc.properties

~~~proper
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://121.196.108.20:3306/mybatis?useUnicode=true&characterEncoding=utf-8&useSSL=false
username=root
password=Hcs1472877.
~~~

MybatisUtils.java

~~~java
public class MybatisUtils {
    private static SqlSessionFactory sqlSessionFactory;

    static {
        try {
            String resource = "mybatis-config.xml";
            InputStream inputStream = getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static SqlSession getSqlSession() {
        return sqlSessionFactory.openSession(true);
    }

~~~

![创建SqlSession](mybatis/%E5%88%9B%E5%BB%BASqlSession.jpg)

## 3. CRUD

### 3.1 namespace

namespace中的包名要和Dao/Mapper接口的包名一致

### 3.2 select

查询语句

- id：接口中对应的方法名
- resultType：接口中方法的返回值
- parameterType：方法的参数类型，多个参数时可以用map作为属性值，并传递参数为Map的对象

~~~xml
<mapper namespace="com.haospring.mapper.UserMapper">
    <select id="getUser" resultType="com.haospring.pojo.User">
        select * from user;
    </select>
    <select id="getUserById" parameterType="int" resultType="com.haospring.pojo.User">
        select * from user where id = #{id}
    </select>
    <insert id="addUser" parameterType="com.haospring.pojo.User">
        insert into user values (null, #{name}, #{pwd});
    </insert>
    <update id="updateUser" parameterType="com.haospring.pojo.User">
        update user set name=#{name},pwd=#{pwd} where id = #{id};
    </update
    <delete id="deleteUserById" parameterType="int">
        delete from user where id = #{id};
    </delete>
</mapper>
~~~

### 3.3 模糊查询

~~~xml
<select id="getUserByLastName" resultType="com.haospring.pojo.User">
    select * from user where name like #{lastName};
</select>	
~~~

## 4. 配置解析

### 4.1 核心配置文件

- mybatis-config.xml

![核心配置文件可用标签](mybatis/%E6%A0%B8%E5%BF%83%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E5%8F%AF%E7%94%A8%E6%A0%87%E7%AD%BE.jpg)

### 4.2 环境配置（environments）

**尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境**

### 4.3 属性（properties）

- 通过properties标签来实现引入配置文件

- 这些属性可以在外部进行配置，并可以进行动态替换。
- 你既可以在典型的 Java 属性文件中配置这些属性
- 也可以在 properties 元素的子元素中设置

方式一：

~~~xml
<properties resource="jdbc.properties"/>
~~~

方式二：

~~~xml
<properties resource="jdbc.properties">
	<property name="username" value="root"/>
    <property name="password" value="password"/>
</properties>
~~~

- 可以直接引入外部文件
- 可以在其中增加一些属性配置
- 如果两个文件有同一个字段，优先使用外部文件的

### 4.4 类型别名（typeAliases）

- 类型别名可为 Java 类型设置一个缩写名字。
- 它仅用于 XML 配置，意在降低冗余的全限定类名书写

两种方式：

1. 配置指定的类

~~~xml
<typeAliases>
	<typeAliases type="com.haospring.pojo.User" alias="User"/>
</typeAliases>
~~~

2. 也可以指定一个包名，MyBatis 会在包名下面搜索需要的 Java Bean

扫描实体类的包，如果没有使用注解，它的默认别名是类的类名首字母小写

如果使用注解，它的别名就是它的注解名

~~~xml
<typeAliases>
	<package name="com.haospring.pojo"/>
</typeAliases>
~~~

在实体类比较少的时候，使用第一种方式

如果实体类十分多，建议使用第二种方式

第一种可以自定义别名，第二种不行，但是可以通过注解自定义别名

@Alias("user")

### 4.5 设置

这是 MyBatis 中极为重要的调整设置，它们会改变 MyBatis 的运行时行为

![开启缓存和懒加载](mybatis/%E5%BC%80%E5%90%AF%E7%BC%93%E5%AD%98%E5%92%8C%E6%87%92%E5%8A%A0%E8%BD%BD.jpg)

![驼峰映射](mybatis/%E9%A9%BC%E5%B3%B0%E6%98%A0%E5%B0%84.jpg)

![日志](mybatis/%E6%97%A5%E5%BF%97.jpg)

### 4.6 映射器（mappers）

MapRegistry：注册绑定mapper文件

方式一：使用resource绑定注册文件

~~~xml
<mappers>
	<mapper resource="UserMapper.xml" />
</mappers>
~~~

方式二：使用class绑定注册文件

~~~xml
<mappers>
	<mapper class="com.haospring.mapper.UserMapper" />
</mappers>
~~~

使用class注意事项：

- 接口和它的配置文件必须同名
- 接口和它的配置文件必须放在同一个包下

方式三：使用扫描包注入

~~~xml
<mappers>
	<package name="com.haospring.mapper"/>
</mappers>
~~~

注意事项和使用class相同

## 5. resultMap

解决实体类的属性名和数据库的字段名不一致的问题

