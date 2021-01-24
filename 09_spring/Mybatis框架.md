# Mybatis框架

## 1. 简介

### 1.1 什么是Mybatis

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
- parameterType：
  - 方法的参数类型，多个参数时可以用map作为属性值，并传递参数为Map的对象
  - 如果参数只有一个，且是基本数据类型或者String类型，可以不加该属性
  - 多个参数可以在方法参数中加上@Param注解

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

结果集映射

~~~xml
id	name		pwd
id	username	password
~~~

~~~xml
<resultMap id="testUserMap" type="testUser">
    <!--<result column="id" property="id"/>-->
    <result column="name" property="username"/>
    <result column="pwd" property="password"/>
</resultMap>

<select id="getUserById" resultMap="testUserMap">
    select *
    from user
    where id = #{id};
</select>
~~~

- 如果列名和属性名不能匹配上，可以在 SELECT 语句中设置列别名

- 使用resultMap映射时可以只映射字段和属性名不一样的部分

## 6. 日志

### 6.1 日志工厂

如果一个数据库操作，出现了异常，需要通过日志排错

![日志](mybatis/%E6%97%A5%E5%BF%97.jpg)

- SLF4J
- LOG4J【掌握】
- LOG4J2
- JDK_LOGGING
- COMMONS_LOGGING
- STDOUT_LOGGING【掌握】
- NO_LOGGING

在mybatis中具体使用哪一个日志实现，在设置中设定，未设置自动查找

STDOUT_LOGGING：标准日志输出

### 6.2 log4j

什么是log4j

- log4j是apache的一个开源项目，通过log4j，可以控制日志信息输送的目的地是控制台、文件、GUI组件

- 可以控制每一条日志的输出格式

- 通过定义每一条日志信息的级别，能够更加细致的控制日志生成过程

- 通过配置文件来灵活配置，不需要修改应用的代码

导入log4j的依赖

~~~xml
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.12</version>
</dependency>
~~~

## 7. 分页

通过分页可以减少数据的处理量

### 7.1 limit分页

~~~sql
# select * from user limit startIndex,pageSize;
select * from user limit 0,2;
~~~

1. 接口

~~~java
List<TestUser> getUserByLimit(Map<String,Integer> map);
~~~

2. 映射文件

~~~xml
<select id="getUserByLimit" parameterType="map" resultType="user">
    select * from user limit #{startIndex},#{pageSize};
</select>
~~~

3. 测试类

~~~java
@Test
public void test2() {
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    TestUserMapper mapper = sqlSession.getMapper(TestUserMapper.class);
    Map<String, Integer> map = new HashMap<>();
    map.put("startIndex", 0);
    map.put("pageSize", 2);
    System.out.println(mapper.getUserByLimit(map));
}
~~~

### 7.2 RowBounds分页

不建议

## 8. 使用注解开发

### 8.1 用例

引入使用注解的接口，将接口注册绑定到mybatis的核心配置文件

~~~xml
<mappers>
    <mapper class="com.haospring.dao.UserMapper"/>
</mappers>
~~~

UserMapper接口，基本的CRUD

~~~java
public interface UserMapper {
    @Select("select * from user")
    List<User> queryAll();

    @Select("select * from user where id=#{id}")
    User queryUserById(Integer id);

    @Insert("insert into user values(null,#{name},#{pwd})")
    int addUser(User user);

    @Update("update user set name=#{name},pwd=#{pwd} where id=#{id}")
    int updateUser(User user);

    @Delete("delete from user where id=#{id}")
    int deleteUser(Integer id);
}

~~~

### 8.2 @Param

- 基本类型的参数或者String类型，需要加上该注解
- 应用数据类型不需要加
- 如果只有一个基本类型的话，可以不加@Param注解，但是建议加上
- 在sql中引用的就是@Param("uid",Integer id)中的uid

~~~java
User queryUserById(@Param("id") Integer id);
~~~

### 8.3 #和$

#{} 能够很大程度上防止sql注入

${} 可能会遇到sql注入

相当于PreparedStatement和Statement的区别

## 9. 多对一

- 多个学生对应一个老师（多对一）
- 一个老师对应多个学生（一对多）

### 9.1 按照查询嵌套处理

相当于子查询

~~~xml
<select id="queryStudentAndTeacher2" resultMap="studentMap2">
    select * from student;
</select>
<resultMap id="studentMap2" type="student" autoMapping="true">
    <association property="teacher" column="tid" javaType="teacher" autoMapping="true" select="queryTeacher"/>
</resultMap>
<select id="queryTeacher" resultType="teacher">
    select * from teacher where id=#{tid}
</select>
~~~

### 9.2 按照结果嵌套查询

相当于多表连接查询

~~~xml
<resultMap id="studentMap" type="student" autoMapping="true">
    <id column="id" property="id"/>
    <association property="teacher" javaType="teacher" autoMapping="true">
        <id column="tid" property="id"/>
        <result column="tname" property="name"/>
    </association>
</resultMap>
<select id="queryStudentAndTeacher" resultMap="studentMap">
    select s.*, t.id tid, t.name, t.name tname
    from student s,
    teacher t
    where s.tid = t.id;
</select>
~~~

## 10. 一对多

### 10.1 按照查询结果映射

~~~xml
<resultMap id="teacherMap" type="teacher" autoMapping="true">
    <collection property="students" autoMapping="true" ofType="student">
        <result column="sid" property="id"/>
        <result column="sname" property="name"/>
    </collection>
</resultMap>
<select id="queryTeacher" resultMap="teacherMap">
    select t.*, s.id sid, s.name sname
    from teacher t,
    student s;
</select>
~~~

### 10.2 小结

1. 关联 - association（多对一，用于成员变量是对象）
2. 集合 - collection（一对多，用户成员变量是集合）
3. javaType & ofType
   1. javaType 用来指定实体类中属性的类型
   2. ofType 用来指定映射到List或者集合中的实体类型，泛型中的约束类型

### 10.3 注意事项

1. 保证sql的可读性
2. 注意一对多和多对一中，属性名和字段名的问题
   1. 如果两张表的字段名相同，会出现映射的结果为主表的情况
   2. 需要起别名，区分两张表的字段

## 11. 动态sql

动态sql就是指根据不同的条件生成不同的sql语句

- if
- choose (when, otherwise)
- trim (where, set)
- foreach

### 11.1 if

~~~xml
<select id="queryAll" resultType="blog">
    select * from blog
    <where>
    	<if test="title!=null">
            and title=#{title}
        </if>
        <if test="author!=null">
            and author=#{author}
        </if>
    </where>
</select>
~~~

### 11.2 choose (when, otherwise)

相当于switch case default

~~~xml
<select id="queryBlogChoose" resultType="blog">
        select * from blog
        <where>
            <choose>
                <when test="title!=null">
                    and title=#{title}
                </when>
                <when test="author!=null">
                    and author=#{author}
                </when>
                <otherwise>
                    and views=#{views}
                </otherwise>
            </choose>
        </where>
    </select>
~~~

### 11.3 trim (where, set)

where元素只会在子元素返回任何内容的情况下才插入 “WHERE” 子句。而且，若子句的开头为 “AND” 或 “OR”，where元素也会将它们去除。

*set* 元素会动态地在行首插入 SET 关键字，并会删掉额外的逗号

~~~xml
<update id="updateBlogSet">
    update blog
    <set>
        <if test="title!=null">
            title=#{title},
        </if>
        <if test="author!=null">
            author=#{author},
        </if>
        <if test="createTime!=null">
            create_time=#{createTime}
        </if>
        <if test="views!=null">
            views=#{views}
        </if>
    </set>
    <where>
        id=#{id}
    </where>
</update>
~~~

### 11.4 sql片段

有时候可能某个 sql 语句我们用的特别多，为了增加代码的重用性，简化代码，我们需要将这些代码抽取出来，然后使用时直接调用。

**提取SQL片段**

~~~xml
<sql id="if-title-author">
   <if test="title != null">
      title = #{title}
   </if>
   <if test="author != null">
      and author = #{author}
   </if>
</sql>
~~~

**引用SQL片段**

~~~xml
<select id="queryBlogIf" parameterType="map" resultType="blog">
  select * from blog
   <where>
       <!-- 引用 sql 片段，如果refid 指定的不在本文件中，那么需要在前面加上 namespace -->
       <include refid="if-title-author"></include>
       <!-- 在这里还可以引用其他的 sql 片段 -->
   </where>
</select>
~~~

### 11.5 Foreach

~~~xml
<select id="queryBlogForeach" parameterType="map" resultType="blog">
  select * from blog
   <where>
       <!--
       collection:指定输入对象中的集合属性
       item:每次遍历生成的对象
       open:开始遍历时的拼接字符串
       close:结束时拼接的字符串
       separator:遍历对象之间需要拼接的字符串
       select * from blog where 1=1 and (id=1 or id=2 or id=3)
     -->
       <foreach collection="ids"  item="id" open="and (" close=")" separator="or">
          id=#{id}
       </foreach>
   </where>
</select>
~~~

