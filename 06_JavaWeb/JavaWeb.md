# JavaWeb

## web应用的框架介绍

- 描述：web应用的开发所使用的框架模式，主要是两种模式：
  - C/S模式 - client/server 客户端/服务器
  - B/S模式 - browser/server 客户端（浏览器）/服务器

### http协议介绍

- 描述：http(Hyper Text Transfer Protocol)超文本传输协议，它是基于TCP/IP协议的一个应用层协议
- 访问tomcat地址
  - http://ip:port/工程名称/想要访问的web资源
  - http://localhost:8080/web_1130/demo01.jsp

## Servlet技术

- 描述：
  - servlet是javaweb中的一种用来处理请求和响应的规范
  - javax.servlet.Servlet
  - 是一个接口
  - 在web工程中定义Servlet，该类是开发者自定义的类名，但是需要继承HttpServlet或者实现Servlet接口

### Request对象

- 描述：Request对象主要用来完成请求的处理，由客户端发送的请求数据都由tomcat封装到Request对象中，所以开发者可以从该对象中获取客户端强请求的数据
- request对象是由HttpServletRequest接口提供的，该接口无需开发者完成实例化，它会定义在servlet中doGet或doPost方法里，以参数的形式

### 常用方法

1. String getParameter()：根据指定页面标签name属性的值获取对应提交的value值
2. String[] getParameterValues()：根据指定页面标签name属性的值获取多个提交的value值，通常该标签checkbox
3. setCharacterEncoding（String）：根据指定的编码集参数设置请求对象中数据的编码集，通常用来解决post请求乱码问题
4. RequestDispatcher getRequestDispatcher（String）：根据指定的字符串类型的地址，完成请求的转发操作；
5. setAttribute(String，Object)：通过指定的键值对，完成对键值对的存储，存储在Request域对象中
6. Object getAttribute(String)：根据指定的字符串类型的key获取request域对象中key所对应的值

### response对象

- 描述
  - javax.servlet.ServletResponse接口
  - 该接口是响应相关的操作，通常在开发中使用的是它的子接口HttpServletResponse
  - 该子接口封装了所有的响应相关的数据，它封装或实例化也是由tomcat完成

#### 常用方法

1. setContentType(String)：设置响应的编码
2. PrintWriter getWriter()：将数据 响应给客户端浏览器
3. write(String)：通过PrintWriter对象调用，向浏览器写出相关信息
4. sendRedirect(String)：根据指定的地址完成重定向访问（request对象重新封装，response对象也会重新封装）

## 会话技术

- 描述：主要指的是用户通过浏览器完成和服务器之间的数据交互

### Cookie

- 描述：Cookie技术不是java独有的，它是w3c指定的一个标准，对于java开发者来说，只是通过java编程语言来实现cookie而已（使用），Cookie对象主要存在于浏览器（Cookie当中的数据通常都是保存到客户端的电脑上，私密性差，建议不要保存敏感数据）
  - javax.servlet.http.Cookie
  - 是一个类，可以直接实例化

### Session

- 描述：JavaWeb中session表示的是客户端浏览器与服务器之间的会话，在javaweb中session的主要作用在服务器临时存储浏览器和服务器会话的数据。

- 总结：

  - session的周期是同一浏览器下会话期间都有效；

  - request的周期是请求到响应期间有效

  - session的时间管理：

    （1）Tomcate默认情况下给session提供的服务器存活时间为30分钟

    （2）开发者通过编码完成时间设置

    - 定义web.xml

~~~xml
<session-config>
    <!-- 单位为分钟 -->
	<session-timeout>60</session-timeout>
</session-config>
~~~

（3）通过方法完成session设置，单位为秒

session.setMaxInactiveInterval(10);

- getSession()：默认为true
- getSession(boolean)：如果为true，表示服务器中存在session对象则直接使用，无需创建新的session对象，如果没有session对象则创建新的session对象；如果为false，意味着服务器中存在session则直接使用，如果服务器中不存在session对象，则不会创建新的session对象

### ApplicationContext

生存周期：只要web服务器不关闭，它就有效

域对象：Request<Aession<ApplicationContext

## 监听器

- 描述：它的主要功能用来监控某个场景动作等；
- JavaWeb中的监听器
  - Web核心对象有哪些：
  - request
  - response
  - session
  - ServletContext
- 可以分为八种监听：
  - 监听ServletContext
  - 监听Session
  - 监听request
  - 监听response
  - 监听他们的创建和销毁（监听它们的生命周期）
- 监听域对象中数据的存储、删除、修改（setAttribute、getAttribute、removeAttribute）：
- 监听session中的JavaBean的操作，session本身的变化

### 监听的使用

通过监听对和新对象的创建和销毁进行监听

和新对象的名字：ServletContext、HttpSession、ServletRequest、ServletResponse

对应的监听名字：ServletContextListener、HttpSessionListener ... 

1. 创建监听类，通常开发者定义的类需要实现监听接口

![ServletContextListener](%E5%9B%BE%E7%89%87/ServletContextListener.jpg)

![ServletContextListener配置](%E5%9B%BE%E7%89%87/ServletContextListener%E9%85%8D%E7%BD%AE.jpg)

2. 将工程部署到tomcat中，启动tomcat，当tomcat启动时就会发现ServletContext 被初始化，当工程被移除或者tomcat关闭时可能会看到ServletContext被销毁
3. 注意事项：Session的监听器只有当访问jsp页面时会看到session初始化信息，因为jsp中内置了session对象；而servlet中没有内置session对象，如果要生成session对象，需要通过request.getSession()方法获取

### 过滤器

- 描述：过滤器主要用来完成拦截客户端（用户）的请求，根据开发者设定的过滤条件，对客户端（用户）的请求进行过滤，只有满足条件才会放行；否则拒绝继续访问
- javax.servlet.Filter，是一个接口，如果开发者想要定义一个过滤器，需要实现该接口
- Filter的使用
  - 自定义过滤器类，实现Filter接口

![Filter](%E5%9B%BE%E7%89%87/Filter.jpg)

完成web.xml对过滤器的配置

过滤器服务启动时，工程会加载web.xml，这是tomcat会加载到web.xml中关于过滤器的配置，并完成初始化；根据web.xml中地址的描述，完成请求的过滤

![Filter2](%E5%9B%BE%E7%89%87/Filter2.jpg)

## Web分层与MVC

### Web的分层

1. control（web）层：处理请求和响应，通常可以用来放置Servlet，获取请求对象，可以从request对象中获取参数对应的值（请求数据），完成响应，通过response对象完成数据响应，响应到浏览器或其它web资源
2. dao层：通过接口的形式完成规范方法的定义
3. daoImpl层：用来实现dao层的接口
4. entity（pojo）层：封装java实体类，通常是用来对应数据库表（类名对应表名、成员变量对应列名）；在过去的开发模式中，该层还可以对应页面的输入项
5. util（tool）层：封装工具类
6. test层：封装测试类
7. service层：用来对应servlet（control）请求，找到对应的dao中的方法，通过服务层可以降低control和dao的耦合性

### MVC架构

M（model）：数据模型，pojo

V（view）：视图，页面（jsp、html），主要针对的是客户端可视化页面

C（controller）：控制器，主要针对的是control层，在当前的javaweb中主要用来存放servlet8