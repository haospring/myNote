# spring mvc框架

## spirng mvc介绍

spring mvc是springframeword的后续产品，主要用来web应用程序功能的开发，它也是框架；主要用来替换传统的javaweb开发中的web层（servlet）；在工程中spring mvc相当于工程中控制层（controller），用来处理请求和响应

spring mvc环境搭建

spring mvc配置文件本身就是spring中的一个组件，因此它采用的是IOC思想

## spring mvc的工作原理

### spring配置文件编程

spring mvc工作核心DispatcherServlet，所有的请求和响应都需要经过DispatcherServlet处理；通俗解释：只要请求能进入DispatcherServlet中，接下来的操作都是spring mvc的事情；

执行步骤如下：

（1）用户发出请求进入工程中web.xml，在web.xml中找到DispatcherServlet（请求的地址必须符合servlet-mapping中url-pattern配置）

（2）进入DispatcherServlet之后，加载springmvc.xml（springmvc的配置文件），首先会将请求分发给HandlerMapping（处理器映射器），这个处理器映射器会分析出具体的执行动作（会去执行拦截器：包含了Handler对象和拦截器），并将执行返回给DispatcherServlet

（3）DispatcherServlet拿到执行之后的返回链，会去找处理器适配器（HandlerAdapter），让适配器去执行每一个不同的Handler模型（就是开发者定义的控制类的对象），Handler对象执行完毕后方法会返回ModelAndView对象（模型视图对象，视图通常指代的是页面，模型只带的是数据），最终适配器获得ModelAndView对象，并将该对象返回给DispatcherServlet

（4）DispatcherServlet继续查找ViewResolve（视图解析器），通过该解析器找到需要执行的视图（页面），并将执行的页面返回给DispatcherServlet

（5）DispatcherServlet找到view（视图）进行渲染，最终DispatcherServlet给用户产生对应的响应数据（将数据放到页面并响应给客户端）

完成自定义处理器对象的开发

修改页面，通过EL表达式完成msg对应的数据显示

### spring注解编程

（1）简单注解用例开发

修改springmvc2.xml

springmvc支持三种返回值类型：

ModelAndView

Void

String：默认标识执行成功后想要转发的地址（页面）；开发者可以在返回值中添加关键字redirect：代表的是重定向，如果开发者只是定义访问地址无任何关键字描述，springmvc会默认执行转发，转发的关键字是forward

String str = "redirect:/helloParam.jsp"

参数绑定：

springmvc框架会自动将页面提交的参数绑定到访问的形参上，根据参数名对应匹配

常用的参数类型：

简单地数据类型：基本数据类型和String类型

HttPServletRequest、

HttPServletResponse

HttpSession

自定义的实体类

### springmvc与json的使用

~~~xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.6</version>
</dependency>
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-core</artifactId>
    <version>2.9.6</version>
</dependency>
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-annotations</artifactId>
    <version>2.9.6</version>
</dependency>
~~~



 

