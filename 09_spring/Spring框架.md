# Spring框架

## spring框架介绍

1. 介绍：spring是一个开源的代码框架，通过该框架可以完成整个工程对象的管理（省去对象实例化的过程），spring完全满足java面向接口的编程思想，所以通常在该框架下开发一定会设计到工程的分层

2. spring的优点

   （2.1）方便解耦（高内聚、低耦合），简化开发（对象和对象的关系、对象的创建都由spring进行管理）

   （2.2）方便测试：spring支持junit，可以直接通过spring的注解开发完成测试

   （2.3）aop编程：面向切面编程，对程序过程进行监控、验证等操作

   （2.4）方便集成其他框架，spring可以支持各种开源框架（mybatis、springmvc等）

   补充说明：降低了javaee开发难度，譬如传统的servlet、jsp，spring对它有了自己的api封装，开发者只需要完成某些标签的引用就可以实现以往相同的功能

## spring的核心技术应用

1. 描述：

   IOC（Inverse Of Control）控制反转，spring通过控制反转，对java对象的创建实现管理，通常在开发中通过控制反转将java对象交给spring的工程完成赋值和对象关系的相关操作；DI依赖注入（通常用来完成赋值，与IOC二者类似）

2. 在maven工程中引入spring的依赖包（jar）

   注意事项：spring各个版本与jdk的兼容问题

   spring 3.*支持jdk5.0以上的版本

   spring 4.*支持jdk6.0以上的版本

   spring 5.*支持jdk8.0以上的版本

4. DI的具体使用方式（spring注入有几种方式）

   （4.1）构造方法注入使用

5. spring的注解及使用

   @Component：任何java类都可以使用该注解

   @Controller：主要用来标注web相关的类（serlvet）

   @Service：主要用来标注service层（譬如：OrderService)

   @Repository：主要用来标注dao层（譬如：OrderDao）

   @Scope：

   总结：在实际开发中，注解不能满足所有的开发需求，通常情况下工程都是注解变成和xml变成同时使用

6. spring的AOP

   （6.1）什么是AOP？

   描述：

   对一个java类如果，开发者想对已经定义完毕的方法或者是功能进行增强，有三种方式：

   （1）继承：子类继承父类，将需要增强功能的方法在子类中重写（纵向增强）

   （2）包装：开发者可以定义一个类，然后将想要增强的类在新定义类中以构造方法参数的形式传递进去，在新类中可以继续增强功能

   （3）JDK的动态代理：在不改变原来类的任何方法的情况下，通过动态代理实现方法的拦截，拦截可以完成方法执行前和方法执行后的功能增强

   Spring如何实现增强？

   AOP（Aspect OrientedPrograming）面向切面编程，它是一个编程思想，aop采用的是横向抽取机制，通过aop可以取代传统的继承方式完成方法功能的增强操作；AOP思想是基于代理的思想，对需要增强的对象创建代理对象，在不修改对象代码的情况下，通过代理对象完成功能的增强操作；（通过AOP在开发中可以实现：性能监视、事务管理、安全检查、缓存、日志记录等）

   （6.2）AOP两种编程方式及相关的名词解释

   AOP的两种编程方式

   spring1.2开始支持aop编程，spring自己封装的aop，是传统的、复杂的开发

   spring2.0之后支持第三方aop框架（AspectJ），所以在开发中通常推荐使用该种方式

   （6.3）AOP相关名词解释

   Joinpoint（连接点）：指代的是那些被拦截的点（就是spring想要增强的方法）

   Pointcut（切入点） ：对那些被拦截的点的具体定义（就是spring中真正需要被代理的方法）

   Advice（通知||增强）：当开发者拦截到连击点后想要做的事情（就是开发者想要增强的具体代码）

   通知可以分为如下几类：

   前置通知（before）：想要被增强的方法运行之前执行的具体代码

   后置通知（afterReturning）：在被增强的方法执行之后运行的具体代码

   异常通知（afterThrowing）：在被增强的方法出现异常是执行的具体代码；

   环绕通知（around）：在被增强的方法执行之前和执行之后都会被执行的具体代码

   After（最终通知）：类似于final，不管什么情况都会执行的具体代码

   declareParaents （引介通知） 几乎用不到；

   

   Introduction （引介） ： 一种特殊的通知，在不修改类代码的前提下可以在运行期间动态的添加一些方法或者是字段

   Target（目标对象） ： 代码的目标对象（代理对象）

   Weaving（织入） ： 把增强引用到目标对象，来创建新的代理对象的过程（spring采用的是动态代理织入，而spring引用的第三方采用编译期织入和类装载期织入）

   Proxy（代理）： 当一个类被aop织入增强后，就会产生一个结果代理类

   如果想要研究代理：推荐jdk的动态代理和CGLIB动态代理

   Jdk代理：基于接口的，生成的目标对象都是接口的派生对象

   CGLIB代理：基于类的，生成的目标对象都是子对象

   ~~~xml
   <!-- 通过bean标签完成UserDao的管理（连接点） -->
   <bean name="userDao" class="com.neu.daoImpl.UserDao"></bean>
   <!-- 通过bean标签管理通知类（封装增强的类） -->
   <bean id="userAdvice" class="com.neu.pojo.UserAdvice"></bean>
   <!-- 通过aop的标签来配置切入点和切面 -->
   <aop:config>
       <!-- 
      配置步骤：
      （1）通过aop：pointcut标签完成切入点的配置，涉及到的属性描述
       id属性：切入点名称（自定义）
       expression属性:该属性用来描述当前具体切入到哪个方法（具体的切入点是谁）
       切入点表达方式有如下集中：
        （1.1）bean(bean id||bean name)：通过该表达式，可以将管理的bean的id属性值或name属性值配置到切入点中
        bea包含的任何方法都会被执行
        （1.2）execution(<访问修饰符>? <返回类型> <方法名>(<参数>)<异常>)：
        execution(* 包名.类名/接口名.方法名(方法参数))
        execution(* com.neu.daoImpl.UserDao.addUser())
        execution(* com.neu.daoImpl..*.addUser(..))代表daoImpl包或子包下的任何类中addUser方法，参数任意
        execution(* com.neu.daoImpl.UserDao.add*(..))代表UserDao类中所有add开头的方法，参数任意
       （2）配置切面（通过标签aop:aspect完成配置）
       ref属性：用来引入切点对应的增强方法
       -->
       <aop:pointcut expression="bean(userDao)" id="mypointcut"/>
       <aop:aspect ref="userAdvice">
       <!-- 
       通过标签完成具体通知的描述，
       通过method属性找到通知对应的方法，
       通过属性pointcut-ref找到最开始定义的切点名称
       -->
           <aop:before method="before" pointcut-ref="mypointcut"/>
           <aop:after method="after" pointcut-ref="mypointcut"/>
           <aop:after-returning method="afterReturning" pointcut-ref="mypointcut"/>
           <aop:around method="around" pointcut-ref="mypointcut"/>
       </aop:aspect>
   </aop:config>
   ~~~

   （6.4）通过注解方式完成AOP的配置

   （6.4.1）编写增强类（UserService）

   （6.4.2）编写通知类（UserServiceAdvice）

加载核心配置文件，核心配置文件中加载jdbc的配置，然后加载数据库环境，通过mappers标签加载映射，生成SqlSessionFacotry接口

select name from tb_student group by course having grade>80;

给按钮加点击事件，事件绑定一个方法，通过该方法将数据传输到后台，调用后天指定方法并返回结果

通过SimpleDateFormat类的构造方法指定格式，调用parse方法格式化该date数据

