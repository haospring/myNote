# jsp

jsp本质上是一个servlet程序

## jsp的头部属性

格式：<%@ page contentType="text/html; charset=utf-8" %>

1. language：表示jsp翻译后是什么语言文件，目前只支持java
2. contentType：表示jsp返回的数据类型是什么，response.setContentType()
3. pageEncoding：表示当前jsp页面本身的字符集
4. import：跟java源代码中一样，用于导包，导类
5. autoflush：设置当out输出流缓冲器满时，是否自动刷新，默认是true
6. buffer：设置缓冲区的大小，默认是8kb
7. errorPage：设置当jsp页面出错时自动跳转到的页面路径
8. isErrorPage：设置当前jsp页面是否是错误信息页面，默认是false，如果是true可以获取异常信息
9. session：设置是否创建HttpSession对象，默认是true
10. extends：设置jsp翻译出来的java类默认继承谁

## jsp常用脚本

1. 声明脚本（极少使用）

   （1）格式：<%!  声明java代码  %>

   （2）作用：可以给jsp翻译出来的java类定义属性和方法甚至是静态代码块。内部类等

![声明脚本](jsp%E5%9B%BE%E7%89%87/%E5%A3%B0%E6%98%8E%E8%84%9A%E6%9C%AC.jpg)

2. 表达式脚本（常用）

   （1）格式：<%=   表达式  %>

   （2）作用：在jsp页面上输出数据

   （3）特点：

   ​		①：所有的表达式脚本都会被翻译到_jspService()方法中

   ​		②：表达式脚本都会被翻译成为out.println()输出到页面上

   ​		③：由于表达式脚本翻译的内容都在\_jspService()方法中，所以_jspService方法中的对象都可以直接使用

   ​		④：表达式脚本中的表达式不能以分号结束

![表达式脚本](jsp%E5%9B%BE%E7%89%87/%E8%A1%A8%E8%BE%BE%E5%BC%8F%E8%84%9A%E6%9C%AC.jpg)

3. 代码脚本

   （1）格式：<%  java语句 %>

   （2）作用：可以再jsp页面中，编写我们需要的语句（写的是java语句）

   （3）特点：

   ​		①：代码脚本翻译之后都在_jspService方法中

   ​		②：代码脚本由于翻译到_jspService方法中，先有对象都可以直接使用

   ​		③：还可以由多个代码脚本块组合完成一个完整的java语句

   ​		④：代码脚本还可以和表达式脚本一起组合使用，在jsp页面上输出数据

![代码脚本](jsp%E5%9B%BE%E7%89%87/%E4%BB%A3%E7%A0%81%E8%84%9A%E6%9C%AC.jpg)

## jsp的九大内置对象

1. HttpServletRequest：request
2. HttpServletResponse：response
3. PageContext：pageContext：jsp的上下文对象
4. HttpSession：session
5. ServletContext：application
6. ServletConfig：config
7. JSPWriter：out：jsp输出流对象
8. Object：page：指向当前jsp的对象
9. Exception：exception

异常类对象需要添加page指令isErrorPage="true"才会生效

### jsp的四大域对象

1. pageContext：PageContext：当前jsp页面有效
2. request：HttpServletRequest：一次请求有效
3. session：HttpSession：一个会话范围内有效
4. application：ServletContext：整个web工程内有效（只要web工程不停止，就有数据）

使用时优先顺序：范围从小到大使用

## 常用标签

### 静态包含

格式：<%@ include file="/include/footer.jsp" %>

特点：

1. 静态包含不会翻译被包含的jsp页面
2. 静态包含其实是把被包含的jsp页面的代码拷贝到包含的位置执行输出

### 动态包含

格式：<jsp:include page = "/include/footer.jsp">\</jsp:include>

特点：

1. 动态包含会把包含的jsp页面也翻译成java代码

### 转发

格式：<jsp:forword page = "/score.jsp">\</jsp:forword>

和servlet的请求转发一样的效果

## EL表达式

说明：Expression Language，是表达式语言

作用：主要是用来替代jsp页面中的表达式脚本，进行数据的输出

格式：

1.表达式脚本<%=request.getAttribute("key") %>

2.EL表达式：${key}

当四个域对象中都有相同的key的数据的时候，EL表达式会按照四个域对象的从小到大的顺序搜索，找到就输出

<% request.setAttribute("p",person) %>

${p.age}：此时通过调用person对象中的getAge方法来获取age属性，如果没有getAge方法则会出错；如果没有age属性，但是有getAge方法，同样能获取到age的值

#### 运算

EL表达式中可以时运运算符

1. 关系运算

   （1）${12 == 12}或​\${12 eq 12}

   （2）${12 != 12}或\${12 ne 12}

   （3）${12 < 12}或\${12 lt 12}

   （4）${12 > 12}或\${12 gt 12}

   （5）${12 <= 12}或\${12 le 12}

   （6）${12 >= 12}或\${12 ge 12}

2. 逻辑运算

   （1）${12 == 12 && 12 > 11}或\${12 == 12 and 12 > 11}

   （1）${12 == 12 || 12 > 11}或\${12 == 12 or 12 > 11}

   （1）${ ! true }或\${ not true }

3. 算数运算

4. empty运算

   可以判断一个数据是否为空，如果为空则输出true，反之false

   （1）值为null值时，为空

   （2）值是空串时，为空

   （3）值是空串Object类型数据，长度为零时，为空

   （4）list集合，元素个数为零时，为空

   （5）map集合，元素个数为零时，为空

   <% request.setAttribute("emptyNull",null); %>

   ${ empty emptyNull}

5. 三元运算

6. "."运算和"[]"运算

### 内置对象

1. pageScope：可以获取pageContext域中的数据
2. requestScope：可以获取request域中的数据
3. sessionScope：可以获取session域中的数据
4. applicationScope：可以获取application域中的数据
5. param：可以获取请求参数的值
6. paramValues：可以获取请求参数的值（多个）

${pagaScope.key}