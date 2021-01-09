# spring5框架

## 1. IOC容器

### 1.1 IOC底层原理

1. Inversion Of Control：控制反转

   (1）把对象创建和对象之间的调用过程，交给Spring进行管理

   (2）使用IOC目的：为了降低耦合度

2. IOC底层原理

   （1）xml解析、工厂模式、反射

![IOC过程](spring/IOC%E8%BF%87%E7%A8%8B.jpg)

### 1.2 IOC接口

1. IOC思想是基于IOC容器完成，IOC容器底层就是对象工厂

2. Spring提供IOC容器实现两种方式：（两个接口）

   （1）BeanFactory：IOC容器基本实现，是Spring内部的使用接口，不提供开发人员进行使用；加载配置文件时不会创建对象，在使用时才会创建对象

   （2）ApplicationContext：BeanFactory接口的子接口，提供更多更强大的功能，一般由开发人员进行使用；加载配置文件时，就会把配置文件中的对象创建

3. ApplicationContext实现类

   （1）FileSystemXmlApplicationContext：使用绝对路径

   （2）ClassPathXmlApplicationContext：使用相对路径

### 1.3 IOC操作Bean管理

1. 什么是Bean管理

   （1）Spring创建对象

   （2）Spring注入属性

2. Bean管理操作有两种方式

   （1）基于xml配置文件方式实现

   （2）基于注解方式实现

#### 1.3.1 基于xml方式

1. **基于xml方式创建对象**

~~~xml
<bean id="user" class="com.haospring.pojo.User"></bean>
~~~

~~~java
ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml");
User user = (User)context.getBean("user");
user.addUser();
~~~

   （1）在spring配置文件中，使用bean标签，标签里面添加对应属性，就可以实现对象的创建

   （2）bean标签常用的属性

   id属性：唯一标识

   class属性：类全路径（包名.类名）

   name属性：和id效果一样，name中可以添加特殊符号，不常用

   scope属性：设置bean的作用域

   属性值：singleton，单例模式，默认值

   prototype，多例模式

   （3）创建对象时，执行默认的无参构造，需要提供无参构造

2. **基于xml方式注入属性**

   **（1）DI：依赖注入，就是注入属性**
   
   方式一：set方法注入
   
~~~xml
<bean id="book" class="com.haospring.pojo.Book">
    <property name="name" value="《白夜行》"></property>
    <property name="price" value="89.9"></property>
</bean>
~~~

   方式二：构造方法注入

   ~~~xml
<bean id="order" class="com.haospring.pojo.Order">
    <constructor-arg name="num" value="abc"></constructor-arg>
    <constructor-arg index="1" value="100.00"></constructor-arg>
</bean>
   ~~~

   **（2）xml注入其他类型属性**

   （2.1）null值

   ~~~xml
<property name="author">
    <null/>
</property>
   ~~~

   （2.2）属性值包含特殊符号

   ~~~xml
<!--
   属性值包含特殊符号
   方式一：转义
   方式二：CDATA区
   -->
<!--<property name="author" value="&lt;东野圭吾&gt;"></property>-->
<property name="author">
    <value><![CDATA[<东野圭吾>]]></value>
</property>
   ~~~

   **（3）注入属性-外部bean**

   ~~~xml
<bean id="userDao" class="com.haospring.dao.impl.UserDaoImpl"></bean>
<bean id="userService" class="com.haospring.service.UserService">
    <property name="userDao" ref="userDao"></property>
</bean>
   ~~~

   **（4）注入属性-内部bean**

   ~~~xml
<!-- 内部bean -->
<bean id="emp" class="com.haospring.pojo.Emp">
    <property name="ename" value="张三"/>
    <property name="gender" value="男"/>
    <property name="dept">
        <bean id="dept" class="com.haospring.pojo.Dept">
            <property name="dname" value="销售"/>
        </bean>
    </property>
</bean>
   ~~~

   **（5）注入属性-集合类型**

   （5.1）注入数组类型属性

   （5.2）注入List集合类型属性

   （5.3）注入Set集合类型属性

   **[注入集合](代码/注入集合.md)**

   **（6）IOC操作Bean管理（FactoryBean）**

   （6.1）普通bean：在配置文件中定义bean类型就是返回类型

   （6.2）工厂bean：在配置文件定义bean类型可以和返回值不一样

​	第一步：创建类，让这个类作为工厂bean，实现接口FactoryBean

​	第二步：实现接口里面的方法，在实现的方法中定义返回的bean类型

~~~java
public class MyBean implements FactoryBean {
    @Override
    public Object getObject() throws Exception {
        Student student = new Student();
        return student;
    }

    @Override
    public Class<?> getObjectType() {
        return null;
    }

    @Override
    public boolean isSingleton() {
        return false;
    }
}
public class TestMyBean {
    @Test
    public void test() {
        ApplicationContext context = new ClassPathXmlApplicationContext("spring3.xml");
        Student student = (Student) context.getBean("myBean");
        System.out.println(student);
        //Student{name='null', age=0, gender='null'}
    }
}
~~~

~~~xml
<bean id="myBean" class="com.haospring.factorybean.MyBean"></bean>
~~~

   **（7）IOC操作Bean管理（bean作用域）**

   在spring里面，默认情况下，bean默认是单实例对象，通过scope属性设置

   scope属性：设置bean的作用域

   属性值：singleton，单例模式，默认值，加载配置文件时就创建对象

   prototype，多例模式，调用getBean方法时创建对象

   request，

   session

~~~xml
<bean id="myBean" class="com.haospring.factorybean.MyBean" scope="prototype"></bean>
~~~

   **（8）IOC操作Bean管理（bean生命周期）**

   （8.1）生命周期是什么

   从对象创建到销毁的过程

   （8.2）bean生命周期

   （8.2.1）通过构造器创建bean实例（无参构造）

   （8.2.2）为bean的属性设置值和对其他bean引用（调用set方法）

   （8.2.3）调用bean的初始化的方法（需要进行配置）

   （8.2.4）bean可以使用了（对象获取到了）

   （8.2.5）当容器关闭时，调用bean的销毁的方法（需要进行配置销毁的方法）

~~~java
package com.haospring.bean;

public class Orders {
    private String oname;
    public Orders() {
        System.out.println("第一步，创建bean的对象");
    }
    public void setOname(String oname) {
        this.oname = oname;
        System.out.println("第二步，调用set方法，给成员变量赋值");
    }
    // 创建执行初始化的方法
    public void initMethod(){
        System.out.println("第三步，配置初始化方法");
    }
    // 创建执行销毁的方法
    public void destroyMethod(){
        System.out.println("第五步，配置销毁方法");
    }
}

public class TestOrders {
    @Test
    public void test() {
        ApplicationContext context = new ClassPathXmlApplicationContext("spring3.xml");
        Orders orders = (Orders) context.getBean("orders");
        System.out.println("第四步，获取创建bean实例对象");
        System.out.println(orders);
        // 手动让bean实例销毁
        ((ClassPathXmlApplicationContext) context).close();
    }
}
~~~

~~~xml
<bean id="orders" class="com.haospring.bean.Orders" init-method="initMethod" destroy-method="destroyMethod">
    <property name="oname" value="订单1"/>
</bean>
~~~

   **（9）IOC操作Bean管理（xml自动装配）**

   （9.1）什么是自动装配

   根据指定装配规则（属性名称或者属性类型）

~~~xml
<!--
    实现自动装配：
        bean标签属性autowire，配置自动装配
        autowire标签两个常用属性值：
            byName根据属性名称注入，注入值bean的id值和类属性名称一样
            byType根据属性类型注入
-->
<bean id="emp" class="com.haospring.autowire.Emp" autowire="byName">
</bean>
<bean id="dept" class="com.haospring.autowire.Dept"></bean>
~~~

   **（10）IOC操作Bean管理（外部属性文件）**

   读取数据库的配置文件

   需要加入名称空间

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:util="http://www.springframework.org/schema/util"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/util https://www.springframework.org/schema/util/spring-util.xsd
                           http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <bean id="druidDataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${prop.driver}"/>
        <property name="url" value="${prop.url}"/>
        <property name="username" value="${prop.user}"/>
        <property name="password" value="${prop.password}"/>
    </bean>
</beans>
~~~

### 1.3.2 基于注解方式

1. **什么是注解**

   （1）注解是代码特殊标记，格式：@注解名称（属性名称=属性值,...）

   （2）使用注解，注解作用在类上面，方法上面，成员变量上面

   （3）使用注解的目的：简化xml配置

2. **Spring针对Bean管理中创建对象提供注解**

   （1）@Component：所有类都可以使用

   （2）@Repository：持久层（dao层）

   （3）@Service：service层

   （4）@Controller：web层（controller层）

   注意：上面四个注解功能是一样的，都可以用来创建bean实例，为了区分，建议按规范写注解

3. 基于注解方式实现对象创建

   第一步：引入依赖

   spring-aop

   第二步：开启组件扫描（需要先引入名称context的空间）

   ~~~xml
   <!-- 开启注解，开启注解扫描时默认开启，所以可以不写 -->
   <context:annotation-config></context:annotation-config>
   <context:component-scan base-package="com.haospring.*"></context:component-scan>
   ~~~

   第三步：给类加注解

   ~~~java
   package com.haospring.service;
   
   import org.springframework.stereotype.Service;
   
   /**
    * 在注解里面value属性值可以不写
    * 默认值为userService
    */
   @Service(value = "userService")
   public class UserService {
       public void add() {
           System.out.println("UserService被扫描到了");
       }
   }
   ~~~

4. **开启组件扫描的细节配置**

   ~~~xml
   <!--
       use-default-filters="false"属性：表示不使用默认的过滤器
       context:include-filter标签：设置扫描哪些内容
       context:exclude-filter标签：设置不扫描哪些内容
   -->
   <!-- 只扫描具有Controller注解的类 -->
   <context:component-scan base-package="com.haospring" use-default-filters="false">
       <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
   </context:component-scan>
   
   <!-- 不扫描具有Component注解的类 -->
   <context:component-scan base-package="com.haospring" use-default-filters="false">
       <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Component"/>
   </context:component-scan>
   ~~~

5. **基于注解方式实现属性注入**

   （1）@Autowired：根据属性类型进行自动装配

   第一步：把service和到对象创建，并在类上都加上注解

   第二步：在service类中注入dao对象，在service添加dao变量，在变量上添加注解

   ~~~java
   public interface UserDao {
       void add();
   }
   
   @Repository(value="userDaoImpl")
   public class UserDaoImpl implements UserDao {
       @Override
       public void add() {
           System.out.println("UserDao add...");
       }
   }
   
   /**
    * 在注解里面value属性值可以不写
    * 默认值为userService
    */
   @Service
   public class UserService {
       @Autowired
       private UserDao userDao;
   
       public void setUserDao(UserDao userDao) {
           this.userDao = userDao;
       }
   
       public void add() {
           System.out.println("UserService被扫描到了");
           userDao.add();
       }
   }
   ~~~

   （2）@Qualifier：根据属性名称进行注入

   该注解和上面@AutoWired一起使用，当一个接口具有多个实现类时，需要制定具体是哪一个实现类

   ~~~java
   @Autowired
   @Qualifier(value="userDaoImpl")
   private UserDao userDao;
   ~~~

   （3）@Resource：既可以根据类型注入，也可以根据名称注入

   不是spring包的注解，是javax包的注解，spring更希望开发者使用上面两个注解
   
   ```java
   // 根据名称注入
   @Resource(name = "userDaoImpl")
   // 根据类型注入
   @Resource
   ```
   
   （4）@Value：注入普通类型属性
   
   ~~~java
   @Value(value="abc")
   private String name;
   ~~~
   
6. **完全注解开发**

   （1）创建配置类，替代xml配置文件

   ~~~java
   @Configuration// 作为配置类，替换xml文件
   @ComponentScan(basePackages = {"com.haospring"})// 开启包扫描
   public class SpringConfig {
   }
   ~~~

   （2）编写测试类

   ~~~java
   public class TestAllAnno {
       @Test
       public void test() {
           // 加载配置类
           ApplicationContext context = new AnnotationConfigApplicationContext(SpringConfig.class);
           UserService userService = context.getBean("userService", UserService.class);
           userService.add();
       }
   }
   ~~~

## 2. AOP

### 2.1 什么是AOP

（1）面向切面编程，利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率

（2）通俗描述：不通过修改源代码的方式在主干功能里面添加新功能

![AOP描述](spring/AOP%E6%8F%8F%E8%BF%B0.jpg)

### 2.2 AOP的底层原理

#### 2.2.1 动态代理

AOP底层使用动态代理

1. 有两种情况动态代理

   （1）有接口情况，使用JDK动态代理

   ![动态代理](spring/JDK%E5%8A%A8%E6%80%81%E4%BB%A3%E7%90%86.jpg)

   （2）没有接口情况，使用CGLIB动态代理

   ![CGLIB动态代理](spring/CGLIB%E5%8A%A8%E6%80%81%E4%BB%A3%E7%90%86.jpg)

2. AOP（JDK动态代理）

   （2.1）使用jdk动态代理，使用Proxy类里面的方法创建代理对象

   ![JDK动态代理API](spring/JDK%E5%8A%A8%E6%80%81%E4%BB%A3%E7%90%86API.jpg)

   第一个参数：类加载器

   第二个参数：增强方法所在的类，这个类实现的接口，支持多个接口

   第三个参数：实现这个接口InvocationHandler，创建代理对象，写增强的方法

   （2.2）编写JDK动态代理代码

   （2.1.1）创建接口，定义方法

   ~~~java
   public interface UserDao {
       public int add(int a, int b);
   
       public String update(String id);
   }
   ~~~

   （2.1.2）创建接口实现类，实现方法

   ~~~java
   public class UserDaoImpl implements UserDao {
       @Override
       public int add(int a, int b) {
           return a + b;
       }
   
       @Override
       public String update(String id) {
           return id;
       }
   }
   ~~~

   （2.2.3）使用Proxy类创建接口代理对象

   [JDK动态代理代码](spring/JDK动态代理代码.md)

### 2.2 AOP术语

1. 连接点
2. 切入点
3. 通知（增强）
4. 切面

#### 2.2.1 连接点

类里面哪些方法可以被增强，这些方法称为连接点

#### 2.2.2 切入点

实际真正被增强的方法，称为切入点

#### 2.2.3 通知（增强）

（1）实际被增强的逻辑部分称为通知（增强）

（2）通知的多种类型

前置通知：被增强的方法执行前执行（before）

后置通知：方法执行后执行（afterReturning），有异常不执行

环绕通知：方法执行前后执行（around），出现异常后，第二部分不执行

异常通知：当方法出现异常才会执行（afterThrowing）

最终通知：一定会执行，类似于finally（after）

#### 2.2.4 切面

是动作，把通知应用到切入点的过程称为切面

### 2.3 AspectJ

#### 2.3.1 什么是AspectJ

AspectJ不是Spring组成部分，独立AOP框架，一般把AspectJ和Spring框架一起使用，进行AOP操作

#### 2.3.2 AspectJ实现AOP操作

1. 基于xml配置文件实现
2. 基于注解方式实现（使用）

#### 2.3.3 切入点表达式

（1）切入点表达式作用：知道对哪个类里面的哪个方法进行增强

（2）语法结构：

execution(\[权限修饰符]\[返回类型]\[类全路径]\[方法名称](参数列表))

e.g. execution(* com.haospring.dao.BookDao.add(..))

e.g. execution(* com.haospring.dao.BookDao.*(..))

e.g. execution(* com.haospring.dao.\*.*(..）)

#### 2.3.4 AOP操作（AspectJ注解）

1. 创建类，在类里面定义方法

~~~java
// 被增强的类
public class User {
    public void add(){
        System.out.println("add......");
    }
}
~~~

2. 创建增强类

   （1）在增强类里面创建方法，让不同方法代表不同通知类型

~~~java
// 增强的类
public class UserProxy {
    public void before(){
        System.out.println("before......");
    }
}

~~~

3. 进行通知的配置

   （1）在spring配置文件中，开启注解扫描

   需要开启context和aop的名称空间

   （2）使用注解创建User和UserProxy的对象

   （3）在增强的类上（UserProxy）添加注解@Aspect

   （4）在spring配置文件中开启生成代理对象

~~~xml
<!-- 开启注解扫描 -->
<context:component-scan base-package="com.haospring.*"/>
<!-- 开启AspectJ生成代理的对象 -->
<aop:aspectj-autoproxy/>
~~~

4. 配置不同类型的通知

   （1）在增强类里面，在作为通知方法上面添加通知类型注解，使用切入点表达式配置

~~~java
@Before(value="execution(* com.haospring.aopAnnotation.User.add(..))")
public void before(){
    System.out.println("before......");
}
~~~

5. 相同的切入点抽取

~~~xml
@Pointcut(value = "execution(* com.haospring.aopAnnotation.User.add(..))")
public void pointDemo(){
}
@Before(value="pointDemo()")
~~~

6. 有多个增强类对同一个方法进行增强，设置增强类优先级

   在增强类上面添加注解@Order(数字类型的值)，值越小，优先级越高，从0开始

   [AspectJ代码](spring/AspectJ代码.md)

   运行结果：

   around before......
   before......
   add......
   aroudn after......
   after......
   afterReturning......

#### 2.3.5 AOP操作（xml配置文件，了解）

1. 创建两个类，增强类和被增强类，创建方法
2. 在spring配置文件中创建两个类对象
3. 在spring配置文件中配置切入点

~~~xml
<!-- 创建两个类的对象 -->
<bean id="book" class="com.haospring.aopXML.Book"/>
<bean id="bookProxy" class="com.haospring.aopXML.BookProxy"/>
<!-- 配置aop增强 -->
<aop:config>
    <!-- 切入点 -->
    <aop:pointcut id="p" expression="execution(* com.haospring.aopXML.Book.buy(..))"/>

    <!-- 配置切面 -->
    <aop:aspect ref="bookProxy">
        <!-- 增强作用在具体的方法上 -->
        <aop:before method="before" pointcut-ref="p"/>
    </aop:aspect>
</aop:config>
~~~

