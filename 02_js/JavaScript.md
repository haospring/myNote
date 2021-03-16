# JavaScript

html、css、js、java、数据库、jdbc；vue、jQuery

## 三种使用js的方式

a、在html中嵌入script标记

~~~html
<script type = "text/javascript"></script>
~~~

b、在标签中嵌入js代码；

~~~html
<input type="button" value="点我" onclick="alert('不要点我')" />
~~~

c、在html中引入外部的js文件；	--推荐使用

~~~html
<script type = "text/javascript" src = "1.js" ></script>
~~~

## js的基本语法

### 基本规则

a、严格==区分大小写==
b、变量是==弱类型==
c、每行代码结尾加分号
d、大括号代表代码块
e、注释简单（//单行注释 /* 多行注释 */）

### 变量常量

a、对于字符串中出现的特殊字符，可以通过==反斜杠\进行转义==；
b、常量和变量
		b1：常量，值不可修改，js中没有常量的概念，某个变量不被修改的话就是一个常量
		b2：变量，值可修改
c、变量使用var声明，也可以不声明

### 变量声明

a、以字母、下划线、美元符号$开头，内容可以是前三种符号加数字
b、最长是255个字符
c、严格区分大小写
d、不能有空格等特殊符号
e、不能使用关键字和保留字

### 变量类型

undefined：某个变量只有声明没有赋值
string：字符串
boolean：布尔
number：数值（NaN，not a number，也是number类型）
null：空
function：函数
object：对象
js可以使用typeof(Object object)获取变量的类型（除了null）
在js中，所有的变量都可以作为一个boolean类型的变量去使用
0为假、null为假、undefined为假、空字符串为假

### 类型转换

js种变量的类型跟值有关，值是什么类型，变量就是什么类型
不同类型的变量可以进行“+”运算，主要是字符串、数字、布尔三种类型
优先级：字符串 > 数字 > 布尔
布尔类型进行数学运算时，true会转为1，false会转为0
字符串转数字，parseInt(),parseFloat(),Number(),前两个只对数字开头的字符串有效，第三个只对全数字的字符串有效

~~~js
b = "3.1a4";
console.log("parseInt(b)=" + parseInt(b));//3
console.log("parseFloat(b)=" + parseFloat(b));//3.1
console.log("Number(b)=" + Number(b));//NaN
~~~

\==：比较值是否相等
\===：绝对相等，比较原始类型

~~~js
a = "123";
b = 123;
console.log("a==b is " + (a == b));//true
console.log("a===b is " + (a === b));//false，判断原始类型
~~~

### 运算符

赋值运算符：=、+=、-=、/=、\*=、%=
算数运算符：+、-、*、/、%、++、--

~~~js
console.log("5/2=" + (x / y));//2.5
console.log("5%2=" + (x % y));//1
~~~

逻辑运算符：&&、||、!
&&：当表达式全为真的时候。返回最后一个表达式的值

~~~js
// js中所有变量都可以作为boolean值
// 0为假，null为假，空字符串为假
var a = "abc";
var b = true;
var d = false;
var c = null;

alert(a&&b);//true
alert(b&&a);//abc
~~~

&&：当表达式中有一个为假时，返回第一个为假的值

~~~js
alert(a&&d);//false
alert(a&&c);//null
alert(a&&d&&c);//false
~~~

||:当表达式全为假时，返回最后一个表达式的值

只要有一个为真，就会返回第一个为真的表达式的值

~~~js
x = 5;
y = 6;
console.log("x>3&&y<7 is " + (x > 3 && y < 7));//true
console.log("x<3||y<7 is " + (x < 3 || y < 7));//true
console.log("!(x>3) is " + !(x > 3));//false
~~~

关系运算符：>、<、==、>=、<=、!=
	结果为布尔类型
三元运算符：表达式1>表达式2？表达式1：表达式2
单目 > 算术 > 位移 > 关系 > 逻辑 > 三目 > 赋值

### 流程控制

#### 分支语句

if
if...else...
if...else if...else if...
switch...case...

#### 循环语句

for
while
do while

document.getElementById("a").value获取的值为字符串，需要转为整型比较大小
a、循环可以嵌套多层，一般建议不超过3层
b、一般使用两层for循环遍历二维数组

#### 终止循环的关键字

break：跳出整个循环
continue：结束当次循环，转而进行下一次循环
return：结束方法

### 函数

1）说明：
	a、把实现一个功能的多条语句放在一起，使用函数名来调用（方法）
	b、函数必须先声明，再被调用才能生效

​	c、js中函数不允许重载，后面的方法会覆盖前面的同名方法

2）声明函数（也叫定义函数、创建函数）的语法：
function 函数名（参数1，参数2，...）{
	函数体代码；
	return 返回值；//如果没有返回值，可以没有本行代码
}

3）arguements对象：
	a、js的语法宽松，允许在定义函数时不提供参数；在调用函数时提供参数；可以在函数体中通过arguements对象来获取对应的参数

~~~js
//类似于java的可变数组public void sum(int...num)
function fun(){
    alert(arguments.length);
    for(var i = 0;i<arguments.length;i++){
        alert(arguments[i]);
    }
}
fun(1,"abc",true);
~~~

4）函数的三种调用方式
	a、三种方式：普通调用、超链接调用、对象的事件调用；

~~~html
<script type = "text/javascript">
    function fun(){
        alert("abc");
    }
</script>

<!-- 超链接调用 -->
<a href = "javascript:fun()"></a>

<script type = "text/javascript">
    //普通调用
    fun();
    //事件调用
    <input type = "button" value= "按钮" onclick = "fun();"/>
</script>
~~~

5）内部函数
	a、js本身在带很多有功能的函数，可以直接调用使用
	b、把字符串转为数字parseInt()、parseFloat()、Number()
	c、isNaN(a)判断a是否是非数字
	d、eval("字符串")：把参数字符串当成表达式执行，并返回表达式的结果

~~~js
//函数的定义方式1
function fun(a,b){
    var sum = a+b;
    return sum;
}
alert(fun(3,4));//7

//函数的定义方式2
var fun = function(a,b){
    var sum = a+b;
    return sum;
}
alert(fun(3,4));//7
~~~

### 对象

1）说明：
	a、js也是一种面向对象的语言，很多值都可以作为对象来使用
	b、对象有属性、有方法：属性表示对象的静态特征，方法表示对象的动态特征（功能）
	c、可以通过 对象名.属性名、对象名.方法名()  来使用属性或方法
	d、对象的创建：可以通过new来创建对象，可以通过js代码获取已有的对象（包括DOM对象）

~~~js
//new object()形式的自定义对象
var obj = new object();
obj.name = "haospring";
obj.age = 18;
obj.fun = function(){
    alert("姓名："+this.name+" 年龄:"+this.age)
}
alert(obj.name);//haospring
obj.fun();//姓名：haospring 年龄：18

//{}形式的自定义对象，空对象
//成员之间用逗号隔开
//var 变量名 = {			空对象
//	属性名：值，			  定义属性
//    属性名：值，
//    属性名：值，
//    函数名：function（）{}  定义函数
//};
var obj = {
  name : "hao",
  age:18,
  fun:function(){
      alert("姓名："+this.name+"年龄："+this.age)
  }
};
alert(obj.name);
alert(obj.fun());

~~~

#### Array

表示创建对象数组
var a = new Array();//创建一个长度为0的数组
var a = new Array(4);//创建长度为4的数组
var b = new Array("aa","bb","cc");//创建有初始值的数组
js中数组==长度可变==
sort()方法默认按照字符串方式排序

~~~js
b.sort(); //默认按照字符串方式排序
console.log("b=" + b);//b=13,2,24,35,5

b.sort(function(a, b) {
	return a - b
})
console.log("b="+b);//b=2,5,13,24,35

var arr = [];//定义一个空数组
arr[0] = 12
alert(arr.length);//12
arr[2] = "abc";//只有赋值时才可以通过下表扩容数组，读取时不行
alert(arr[9]);//underfined
alert(arr.length);//3
alert(arr[2]);//abc
alert(arr.length)//3
alert(arr[1]);//undefined
~~~

#### Date
表示日期和时间，可以通过api获取年、月、日、时、分、秒等值
​创建表示当前日期和时间的对象：var d = new Date();

~~~js
var a = new Date(); //当前日期和时间
var b = new Date(2020, 11, 11); //表示2020年12月11日，月份比实际值小1,0到11月份
var c = new Date("2020/11/11");//2020年11月11日
//获取各种值得方法：
//getYear():获取当前年（小于2000年的只显示后两位）
//getFullYear():获取年份的全四位数
//getMonth():获取月份，从0到11，可以手动加1得到真正月份值
//getDate():获取多少号
//getDay():获取一周的星期几，周日是0
//getHours():获取小时
//getMinutes():获取分钟
//getSeconds():获取秒
~~~

#### Math
使用Math时不需要创建对象，直接通过Math，来调用各种方法
​功能：提供js中进行数学运算的相关方法
​Math的属性：LN10、PI、SQTR1_2

~~~ js
var a = 3.14159;
console.log("a="+a);
console.log("Math.LN10="+Math.LN10);//2.302585092994046
console.log("Math.PI="+Math.PI);//3.141592653589793
console.log("Math.SQRT1_2="+Math.SQRT1_2);//0.7071067811865476
//abs()：绝对值
//ceil()：向上取整
//floor()：向下取整
//found()：四舍五入
//pow(x,a)：x^a；
//sqrt()：平方根
a.toFixed(3)//保留小数点后三位
//random()：0.0<=x<1.0的随机数
~~~

#### String
length属性：表示字符串的长度

~~~js
// charAt(int index):获取指定索引的字符
// concat(string str):连接字符串
// indexOf(string str):返回String对象内第一次出现子字符串的字符索引，通常用来判断是否包含子字符串
// lastIndexOf(string str):返回String对象中最后一次出现的字符索引
// replace(str1,str2):返回str1替换为str2后的新字符串，原字符串不变
// split():根据指定字符把字符串分割成数组
// substr(start,length):从start开始截取length长度的子字符串返回
// substring(start,end)从start开始截取到end位置的子字符串返回，包含start，不包含end
// toLowerCase():字符串全部小写
// toUpperCase():字符串全部大写
~~~

#### Document

~~~ html
<script type = text/javascript>
    // getElementById()
    // getElementsByName()
    // getElementsByTagName()
    // innerHTML起始标签和结束标签中间的内容，这个属性可读可写

    // 全选
    function selectAll(){
		var hobbies = document.getElementsByName("hobby");
        for(var i = 0;i<hobbies.length;i++){
            hobbies[i].checked = true;
        }
    }
    
    // 全不选
    function selectNo(){
        var hobbies = document.getElementsByName("hobby");
        for(var i = 0;i<hobbies.length;i++){
            hobbies[i].checked = false;
        }
    }
    
    // 反选
    function selectReverse(){
        var hobbies = document.getElementsByName("hobby");
        for (var i = 0; i < hobbies.length; i++) {
      		//     if (hobbies[i].checked) {
      		//         hobbies[i].checked = false;
       		//     } else {
       		//         hobbies[i].checked = true;
       		//     }
            hobbies[i].checked = !hobbies[i].checked;
        }
        
    }
</script>

<input type = "checkbox" name = "hobby" value = "swimming" />游泳
<input type = "checkbox" name = "hobby" value = "game" />游戏
<input type = "checkbox" name = "hobby" value = "basketball" />
<button onclick="selectAll();">全选</button>
<button onclick="selectNo();">全不选</button>
<button onclick="selectReverse();">反选</button>
~~~

- 属性：

  - childNodes：获取当前节点的所有子节点
    - 标签之间的空白处也算一个节点
  - firstChild：获取当前节点的第一个子节点
  - lastChild：获取当前节点的最后一个子节点
  - parentNode：获取当前节点的父节点
  - nextSibling：获取当前节点的下一个节点
  - previousSibling：获取当前节点的上一个节点
  - className：用于获取或设置标签的class属性值
  - innerHTML：表示获取/设置起始标签和结束标签之间的内容
  - innerText：表示获取/设置起始标签和结束标签之间的文本内容
  - body：body标签对象，需要在页面加载完毕后使用

- 方法：

  - appendChild(oChildNode)：添加一个子节点
  - createElement()

  ~~~js
  // 页面加载完后才能读取document.body
  window.load = function(){
      // 方式一：
      var divObj = document.createElement("div");//在内存中，页面显示不出来
      divObj.innerHTML = "haospring";//给创建的div对象添加内容，仍在内存中
      // document中提供了body属性，它代表body对象
      document.body.appendChild(divObj);//将div对象添加到body中
      
      // 方式二：
      var div = document.createElement("div");// 创建一个div节点对象
      var textNode = document.createTextNode("haospring");// 创建一个文本节点对象
      div.appendChild(textNode);// 将文本加点添加到div节点上
      document.body.appendChild(div);// 将div节点添加到body上
  }
  ~~~

- 注意：

  - 标签中的文本也是一个对象

### 表单有效性验证

1）说明：
	a、有效性认证：在表单提交之前，验证表单域值应该符合某些格式规定，称为有效性验证
	b、一般在客户端上通过js进行有效性验证
	c、通常两种触发校验的方式：表单域的onchange或者onblur等事件、表单的onsubmit事件

2）简单的校验，程序员自己写校验格式代码

### 正则表达式

是一种描述字符模式的对象，很多语言都支持正则表达式的运用
通常在js中使用正则表达式来完成表单的有效性验证

~~~ js
/^\d{6}$/
//^表示行开头
//$表示行结尾
//普通字符
[多个字符]：表示字符串要包含中括号里面的字符
	[A-Z]、[a-z]
[^多个字符]：表示字符串不能包含中括号^后面的字符
	[^A-Z]、[^a-z]
\d：任何数字
\D：非数字
\w：字母数字下划线：[a-zA-Z0-9_]
\W：表示任意一个非单字字符
\s：表示匹配所有空白符
\S：表示非空白符，包括换行
{数字}：表示出现次数
//特殊字符
+：表示前面的字符必须至少出现一次（1次或多次）
*：表示前面的字符可以不出现，也可以出现一次或者多次（0次、或1次、或多次）
?：表示前面的字符最多只可以出现一次（0次、或1次）
.：表示回车换行之外的任意一个字符
|：表示两项之间的一个选择
//限定符
+：表示前面的字符必须至少出现一次（1次或多次）
*：表示前面的字符可以不出现，也可以出现一次或者多次（0次、或1次、或多次）
?：表示前面的字符最多只可以出现一次（0次、或1次）
{n}：n 是一个非负整数。匹配确定的 n 次。例如，'o{2}' 不能匹配 "Bob" 中的 'o'，但是能匹配 "food" 中的两个 o。
{n,}：n 是一个非负整数。至少匹配n 次。例如，'o{2,}' 不能匹配 "Bob" 中的 'o'，但能匹配 "foooood" 中的所有 o。'o{1,}' 等价于 'o+'。'o{0,}' 则等价于 'o*'
{n,m}：m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。例如，"o{1,3}" 将匹配 "fooooood" 中的前三个 o。'o{0,1}' 等价于 'o?'。请注意在逗号和两个数之间不能有空格。

//验证邮政编码：/^\d{6}$/
//验证固定电话：/^\d{3}-\d{8}$|^d{4}-\d{8}$/
//验证身份证号码：/^\d{18}$|^\d{17}[xX]$/		
//验证电子邮箱地址：/^\w+((-\w+)|(\.\w+))*\@[A-Za-z0-9]+((\.|-)[A-Za-z0-9]+)*\.[A-Za-z0-9]+$/

// 验证字符串是否由字母、下划线组成，且为5-12位
var pattern = "[^\w{5,12}$]";
var name = document.getElementById("name");
var nameValue = name.value;
pattern.test(nameValue);
// test()方法用来判断字符串是否匹配规则，是则返回true，否则false
~~~

### js的对象模型

#### BOM

Browser Object Model

浏览器对象模型：把浏览器中所有的东西都当成对象来使用
以windows对象作为跟对象，有document、history、location等子对象，可以直接使用
window是顶级对象，可以省略不写

#### DOM

Document Object Model
基本的三个交互函数
	alert()
	prompt()
	confirm()
定时函数：
	setTimeOut("函数名",间隔时间)：需要递归方式调用
	clearTimeout()停止定时器
	setInerval("函数名",间隔时间)：直接调用

### 事件

事件：在页面中，进行鼠标点击、或者键盘按键的输入等操作
事件处理：当某个事件发生时，要做的事（通常对应我们定义的js函数）
窗口或者页面的事件：onblur、onfocus、onload等
键盘或者鼠标的事件：
	onclick：鼠标点击
	onDbClick：鼠标双击
	onKeyPress：按键按下并抬起
	onKeyDown：按键按下
	onKeyUp：按键抬起
	onMouseMove：鼠标移动
	onMouseOver:
表单元素的事件：onfocus、onblur、onchange、onclick、onsubmit等



- onload：加载完成事件

  - 页面加载完成之后，常用于做js代码初始化操作

  ~~~html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <script type="text/javascript">
          // function fun(){
          //     alert("静态注册onload事件，所有代码");
          // }
  
          window.onload = function(){
              alert("动态注册onload事件，所有代码");
          }
      </script>
  </head>
  <!--<body onload="fun();">-->
  <body>
  </body>
  </html>
  ~~~

- onclick：单击事件

  - 常用于按钮的单击响应操作

  ~~~html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <script type="text/javascript">
          /*function fun() {
              alert("静态注册onclick事件");
          }*/
  
          window.onload = function () {
              // 1、获取标签对象
              let btn = document.getElementById("btn");
              // 2、通过 对象名.事件名= function(){}
              btn.onclick = function () {
                  alert("按钮1的事件");
              }
  
              var btn2 = document.getElementById("btn2");
              btn2.onclick = function () {
                  alert("按钮2的事件");
              }
  
          }
      </script>
  </head>
  <body>
  <!--<button onclick="fun();">按钮</button>-->
  <button id="btn">按钮1</button>
  <button id="btn2">按钮2</button>
  </body>
  </html>
  ~~~

- onblur：失去焦点事件

  - 常用于输入框失去焦点后验证其输入内容是否合法

  ~~~html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
  
      <script type="text/javascript">
          function onblurFun(){
              alert("静态注册onblur事件");
          }
  
          window.onload = function () {
              var psw = document.getElementById("password");
              psw.onblur = function () {
                  alert("动态注册onblur事件");
              }
          }
      </script>
  </head>
  <body>
  	用户名:<input type="text" onblur="onblurFun();"><br/>
  	密码:<input id="password" type="text"><br/>
  </body>
  </html>
  ~~~

- onchange：内容发生改变事件

  - 常用于下拉列表和输入框内容发生改变后操作

  ~~~html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
  
      <script type="text/javascript">
          function onchangeFun() {
              alert("女神已经改变了");
          }
  
          window.onload = function () {
              //1 获取标签对象
              var selObj = document.getElementById("sel01");
              // alert( selObj );
              //2 通过标签对象.事件名 = function(){}
              selObj.onchange = function () {
                  alert("男神已经改变了");
              }
          }
  
      </script>
  </head>
  <body>
  请选择你心中的女神：
  <!--静态注册onchange事件-->
  <select onchange="onchangeFun();">
      <option>--女神--</option>
      <option>芳芳</option>
      <option>佳佳</option>
      <option>娘娘</option>
  </select>
  
  请选择你心中的男神：
  <select id="sel01">
      <option>--男神--</option>
      <option>国哥</option>
      <option>华仔</option>
      <option>富城</option>
  </select>
  
  </body>
  </html>
  ~~~

- onsubmit：

  -  常用于表单提交前，验证所有表单项是否合法

  ~~~html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
     
      <script type="text/javascript">
          // 通过onsubmit事件校验表达是否合法，如果不合法则阻止提交
          function onsubmitFun() {
              alert("表单校验不合法，阻止表单提交");
              return false;
          }
  
          window.onload = function () {
              var form01 = document.getElementById("form01");
              form01.onsubmit = function () {
                  alert("动态提交");
                  return false;
              }
          }
      </script>
  </head>
  
  <body>
  <form action="http://localhost:8080" method="get" onsubmit="return onsubmitFun();">
      <input type="submit" value="静态注册"/>
  </form>
  <form action="http://localhost:8080" method="get" id="form01">
      <input type="submit" value="动态注册"/>
  </form>
  </body>
  </html>
  ~~~

  





