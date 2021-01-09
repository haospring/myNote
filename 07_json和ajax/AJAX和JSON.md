# AJAX和JSON

## JSON

**什么是json?**

JSON-JavaScript Object Notation：js对象的表示法（数据定义格式），轻量级文本数据交互，json是独立的语言，所以开发者在使用json时需要引入json库

**json作用：**
完成客户端和服务端、或者是不同服务端之间数据传输；早期的数据传递使用的是xml

**xml数据格式：**

~~~xml
<student>
	<name>张三</name>
    <age>18</age>
    <score>89</score>
</student>
~~~

**json的数据格式：**

~~~json
[student{
 name:张三,
 age:18,
 score:89
 }]
~~~

json语法是javascript对象表示语法的子集，数据是以键值对的形式进行描述：属性名：属性值，不同的属性之间通过“，”分隔，大括号作为数据对象的保存符号，中括号代表数组

数据格式：

1. 不包括数组{属性1：值1，属性2：值2，...}，最后一行键值对后没有任何结束符号
2. 包括数组[{属性1：值1，属性2：值2，...}，...]

- 注意事项：json数据中，key必须由双引号引用，对应的value具备数据类型类型如下：
  - 数字（整数、浮点）
  - 字符串（双引号）
  - 逻辑值（true、false）
  - 数组（具备中括号）
  - 对象（具备大括号）
  - null

![json](json%E5%9B%BE%E7%89%87/json.jpg)

## AJAX

- 描述：
  - ajax：asynchronous javascript and xml 异步处理脚本；
  - ajax无需重新加载整个网页就可以获取部分数据显示的脚本语言（异步处理），可以实现网页的局部刷新
  - ajax本质不是一个新技术，它只是将传统的js、xml（text）进行了封装，在页面不刷新的情况下，可以和服务器进行交互获得数据，显示在页面上

- 使用：

  - 创建ajax的核心对象XMLHttpRequest

    （1）XMLHttpRequest是ajax的核心对象，该核心对象又是浏览器用于访问web服务器的核心对象；核心对象在创建时通常分为两种情况

    （2）现代浏览器（firefox、chrome、ie7以后的浏览器），核心对象是XMLHttpRequest

    （3）老版本浏览器（ie6之前），核心对象是ActiveX

![ajax](ajax%E5%9B%BE%E7%89%87/ajax.jpg)

2. ajax和servlet之间的访问

   （1）返回text文本

![返回text](ajax%E5%9B%BE%E7%89%87/%E8%BF%94%E5%9B%9Etext.jpg)

3. 返回json类型的数据