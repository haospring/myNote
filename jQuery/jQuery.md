# jQuery

- 描述：JavaScript和查询（Query），它就是辅助JavaScript开发的js类库

~~~js
<script type="text/javascript" src = "../../script/jquery-1.7.2.js"></script>
<script type = "text/javascript">
    $(function () {//表示页面加载完成之后，相当于window.onload = function(){}事件
        var $btn = $("#btn");//表示按id标签查找对象
        $btn.click(function(){//绑定点击事件
            alert("jQuery的单击事件");
        });
	});
</script>
~~~

- jQuery的$符号是一个函数

## jQuery核心函数

\$是jquery的核心函数，能完成jquery的很多功能。\$()就是调用$这个函数

- 传入参数为[函数]时：

  - 表示页面加载完成之后。相当于window.onload = function(){}

  ~~~js
  $(function(){
      alert("页面加载完成后自动执行");
  });
  ~~~

- 传入参数为[HTML字符串]时：

  - 根据这个字符串创建元素节点对象

  ~~~js
  $("    <div>" +
              "        <span>div-span1</span>" +
              "        <span>div-span2</span>" +
              "    </div>").appendTo("body");
  ~~~

- 传入参数为[选择器字符串]时：

  - 根据这个字符串查找元素节点对象

  ~~~js
  // $("#id属性值");id选择器，根据id查询标签对象
  // $("标签名");标签选择器，根据标签名查询标签对象
  // $(".类名");类选择器，根据类名查询标签对象
  alert($("button").length);
  ~~~

- 传入参数为[DOM对象]时：

  - 将DOM对象包装为jQuery对象返回

  ~~~js
  var btnObj = document.getElementById("btn01");
  alert($(btnObj));
  ~~~

## jQuery的本质

- jquery对象是dom对象的数组+jQuery提供的一系列功能函数

  ~~~html
  <script type="text/javascript" src = "../../script/jquery-1.7.2.js"></script>
  <script type = "text/javascript">
      $(function () {
          var $btns = $("button");
          for(var i = 0;i<$btns.length;i++){
              alert($btns[i]);
          }
      });
  </script>
  
  <body>
     <button id="btn01">按钮1</button>
     <button id="btn02">按钮2</button>
     <button id="btn03">按钮3</button>
     <button id="btn04">按钮4</button>
  </body>
  ~~~

## Dom对象和jQuery对象的转换

- dom对象转jquery对象
  - 先有dom对象
  - $(dom对象);
- jQuery对象转dom对象
  - 先有jQuery对象
  - jQuery对象[下标]得到对应的dom对象

## 选择器

### 基本选择器

#ID			选择器：根据id查找标签对象

.class 		选择器：根据class查找标签对象

element	选择器：根据标签查找标签对象

\*				选择器：表示任意的，所有的元素

selector1,selector2 组合选择器：合并选择器1，选择器2的结果并返回

prev+next 该元素的下一个兄弟元素

prev~next 该元素的之后的所有兄弟元素

~~~js
$("#id");
$(".myClass");
$("button");
$("*");
$("div,span,p.myClass");
$(function(){
    $("#btn01").click(function(){
    	$("#one").css("background-color","red");
	});
});
// 后代选择器
$("form input");// form里所有的input元素
// 子元素选择器
$("form > input");// form里的子元素input
// 紧挨着另一个元素的元素
$("label+input");
// 后面所有兄弟元素
$("form ~ input");
~~~

### 过滤选择器

#### 基本选择器

- ：first		获取第一个元素
- ：last         获取最后一个元素
- ：not         去除所有与给定选择器匹配的元素
- ：even       匹配所有索引值为偶数的元素，从0开始计数
- ：odd        匹配所有索引值为奇数的元素，从0开始计数
- ：eq(index)          匹配一个给定索引值的元素,index表示从0开始计数
- ：gt(index)           匹配大于给定索引值的元素
- ：lt(index)            匹配小于给定索引值的元素
- ：header              匹配h1、h2、h3之类的标题元素
- ：animated          匹配正在执行动画的所有元素

~~~html
<ul>
	<li>list item1</li>
    <li>list item2</li>
    <li>list item3</li>
    <li>list item4</li>
</ul>
<input name = "apple" />
<input name = "banaba" checked = "checked" />

<script type = "text/javascript" src = "../../script/script/jquery-1.7.2.js"></script>

<scirpt type = "text/javascript">
	alert($("li:first"));
    $("input:not(:checked)");
    $("li:even");// 获取到list item1和list item3
    $("li:odd");
    $(li:eq(1));// list item2
    $("li:lt(2)");
    $("li:gt(1)");
</scirpt>
~~~

#### 内容过滤器

- ：containts			匹配包含给定文本的元素
- ：empty                 匹配所有不包含子元素或者文本的空元素
- ：parent                 匹配含有子元素或者文本的元素
- ：has(selector)      匹配含有选择器所匹配的元素的元素，selector一个用于筛选的选择器

~~~html
<div>John Resig</div>
<div>George Martin</div>
<div>Malcom John Sinclair</div>
<div></div>
<div><p>Hello</p></div>

<script type = "text/javascript" src = "../../script/jquery-1.7.2.js"></script>
<script type = "text/javascript">
	$("div:contains('John')");
    $("div:empty");
    $("div:parent");
    $("div:has(p)");
</script>
~~~

#### 属性过滤器

- [attribute]			          	匹配包含给定属性的元素
- [attribute = value]            匹配给定的属性是某个特定值的元素
- [attribute != value]           匹配所有不含有指定的属性，或者属性不等于特定值的元素
- [attribute ^= value]          匹配给定的属性是以给定的值开头
- [attribute $= value]          匹配给定的属性是以给定的值结尾
- [attribtue *= value]          匹配给定的属性是以包含某些值的元素
- \[selector1][selector2]      复合选择器，需要同时满足多个条件时使用

~~~html
<div>Hello</div>
<div id = "test">World</div>

<script type = "text/javascript" src = "../../script/jquery-1.7.2.js"></script>
<script type = "text/javascript">
	$("div[id]");
    $("div[id = 'test']");
    $("div[name != 'test']");
    $("div[name ^= 'te']");
    $("div[name $= 'st']");
    $("div[name *= 'es']");
    $("input[id][name $= 'man']");
</script>
~~~

#### 表单过滤器

- ：input				匹配所有input，textarea，select和button元素
- ：text                   匹配所有的单行文本框
- ：password
- ：radio
- ：checkbox
- ：image
- ：reset
- ：submit
- ：button
- ：file
- ：hidden

~~~html
<form>
    <input type = "text" />
    <input type = "checkbox" />
    <input type = "radio" />
    <input type = "submit" />
    <input type = "button" />
    <input type = "image" />
    <input type = "file" />
    <input type = "password" />
    <select>
        <option></option>
    </select>
    <textarea></textarea>
    <button></button>
</form>

<script type = "text/javascript" src = "../../script/jquery-1.7.2.js"></script>
<script type = "text/javascript">
	$(":input");
    $(":checkbox");
</script>
~~~

#### 表单对象属性过滤器

- ：enable				匹配所有可用元素
- ：disabled             匹配所有不可用元素
- ：checked             匹配所有的被选中元素（复选框、单选框，不包括select中的option）
- ：selected             匹配所有选中的option元素

~~~js
$("input:enable");
$("input:disabled");
$("input:checked");
$("select option:selected");

// val()方法可以操作表单项的value属性值
// 它可以设置和获取
$(":text:enable").val("获取可用的文本框并赋值");

// 获取多选框已选择的个数
alert($(":checkbox:checked").length);

// 获取多选框选择的内容
// 1、获取全部选中的复选框对象
var $checkboxes = $(":checkbox:checked");
// 2、遍历复选框对象
for(var i = 0;i<$checkboxes.length;i++){
    // 3、通过dom对象获取value值
    alert($checkboxes[i].value);
}
// jQuery替换遍历each()方法
// 在便来的function函数中，有一个this对象，这个this对象就是当前获取到的dom对象
$checkboxes.each(function(){
    alert(this.value);
});

// 获取下拉框选中的内容
var $options = $("select option:selected");
$options.each(function(){
    alert(this.innerHTML);
});
~~~

## 元素筛选

- eq(index)				相当于:eq(index)
- first()
- last()
- filter(expr)              筛选出与指定表达式匹配的元素集合
- is(expr)                    判断是否匹配给定的表达式
- has(expr)
- not(expr) 
- children(expr)        返回匹配给定选择器
- find(expr)                搜索所有与指定表达式匹配的元素，多用来查找后代
- next()                       prev+next
- nextAll()                   prev~next
- nextUntil()              当前元素到指定元素为止的所有元素
- parent()                   父元素
- prev()                       前一个兄弟元素
- prevAll()
- prevUntil()
- siblings()                 所有的兄弟元素

~~~html
<ul>
    <li>list item1</li>
    <li>list item2</li>
    <li>list item3</li>
    <li>list item4</li>
    <li>list item5</li>
</ul>
<form>
    <input type = "checkbox" />
</form>
<div>
    div<span>div中的span</span>
</div>

<script type = "text/javascript" src = "../../script/jquery-1.7.2.js"></script>
<script type = "text/javascript">
	$("li").eq(2);
    $("li").first();
    $("li").filter(".btn");
    $("li").is("form");
    $("input[type = 'checkbox']").parent().is("form");
    $("div").has("span");
    $("p").find("span");
</script>
~~~

## jQuery的属性操作

- html()				设置和获取起始标签和结束标签之间的内容，相当于innerHTML
- text()				  设置和获取起始标签和结束标签之间的文本，相当于innerText
- val()					设置和获取表单项的value值，和value一样，还可以设置多个表单项的选中状态
- attr()				   可以设置和获取属性的值（不推荐操作checked、readonly、selected、disabled等）
- prop()                 可以设置和获取属性的值（只推荐上面不操作的）

~~~html
<script type = "text/javascript" src = "../../script/jquery-1.7.2.js"></script>
<script>
	$(function(){
        // 不传参数是获取，传入数据是设置
        $("div").html();
        $("div").html("<h1>我是div中的标题1</h1>");
        $("div").text();
        // 设置选中状态
        $(":radio").val(['male']);
        $("#mul").val(["安徽","吉林","辽宁"]);
        // 前后没有顺序要求
        $(":radio,#mul").val(["male","安徽"]);
        $(":radio,#mul").val(["安徽","male"]);
    });
</script>

<script>
	$(function(){
        $(":radio").attr("name");// 获取属性的值
        $(":radio").attr("name","sex");// 设置name属性的值为sex
        // 此时并没有给单选框设置checked属性
        alert($(":radio").attr("checked"));// undifined
        alert($(":radio").prop("checked"));// false
        $(":radio").prop("checked",true);
        $(":radio:first").attr("abc","abcValue");// 添加自定义属性
    });
</script>

<div>
    我是div
    <span>我是div中的span</span>
</div>
<input type = "radio" name = gender value = "male">男
<input type = "raido" name = gender value = "female">女<br/>

<select id = "mul" multiple = "multiple" size = "4">
    <option value = "安徽">安徽</option>
    <option value = "辽宁">辽宁</option>
    <option value = "吉林">吉林</option>
    <option value = "黑龙江">黑龙江</option>
</select>
~~~

**[选择器练习代码](./jQuery代码/选择器练习代码.md)**

## dom的增、删、改

### 内部插入

- appendTo()				a.appendTo(b)			把a插入到b子元素末尾，成为最后一个子元素
- prependTo()              a.prependTo()              把a插入到b所有子元素前面，成为第一个子元素

~~~ html
<script type = "text/javascipt">
	$("<h1>标题</h1>").appendTo("div");
	$("<h1>标题2</h1>").prependTo("div");
	//------------------
	$("<h1>标题</h1>").appendTo($("div"));
</script>
<div>
    1234
</div>
~~~

### 外部插入

- insertAfter()			a.insertAfter(b)			得到ba
- insertBefore()         a.insertBefore(b)         得到ab

~~~ html
<script type = "text/javascipt">
	$("<h1>标题</h1>").insertAfter("div");
	$("<h1>标题2</h1>").insertBefore("div");
</script>
<div>
    1234
</div>
~~~

### 替换

- replaceWith()			a.replaceWith(b)			用b替换a，把多个a替换为一个b
- replaceAll()                a.replaceAll(b)                用a替换所有的b，多个a到多个b

~~~ html
<script type = "text/javascipt">
	$("div").replaceWith($("<h1>标题</h1>"));// 两个div变成1个标题
	$("<h1>标题</h1>").replaceAll("div");// 两个div变成两个标题
</script>
<div>1234</div>
<div>1234</div>
~~~

### 删除

- remove()			a.remove()				删除a标签
- empty()              a.empty()                   清空a标签里的内容包括子标签

~~~html
<script type = "text/javascipt">
	$("div").remove();
	$("div").empty;
</script>
<div>1234</div>
<div>1234</div>
~~~

**[左右添加](./jQuery代码/左右添加.md)**

```js
// confirm()是JavaScript提供的一个确认提示框函数
confirm("haospring");
```

**[添加删除记录](./jQuery代码/添加删除记录.md)**

## CSS样式操作

- addClass()					添加样式

- removeClass()			 删除样式

- toggleClass()				有就删除，没有就添加样式

- offset()						  获取和设置元素的坐标

相当于写好样式后，将样式的类名添加给标签

~~~html
<head>
    <style type = 'text/css'>
        div.redDiv{
            border:2px solid red;
        }
    </style>
    <script type = "text/javascript">
        var $divEle = $("div:eq(0)");
        
        $("#btn01").click(function(){
            $divEle.addClass("redDiv");
        });
        
        $("#btn02").click(function(){
            $divEle.removeClass("redDiv");
            // 删除全部class
            $divEle.removeClass();
        });
    </script>
</head>
<body>
    <div></div>
    <button id = btn01>addClass()</button>
    <button id = btn02>removeClass()</button>
</body>
~~~

## jQuery动画

### 基本动画

- show()					将影藏的元素显示

- hide()					  将可见的元素隐藏

- toggle()				   可见就隐藏，不可见就显示

以上动画方法都可以添加参数

1、第一个参数是动画执行的时长，以毫秒为单位

2、第二个参数是动画的回调函数（动画完成后自动调用的函数）

**[品牌展示](./jQuery代码/品牌练习.md)**

### 淡入淡出动画

- fadeIn()				淡入（慢慢可见）

- fadeOut()			淡出（慢慢消失）

- fadeTo()              在指定的时长内慢慢的将透明度修改到指定的值0-1
- fadeToggle()       淡入/淡出 切换

参数添加同上，fadeTo的参数为：(时长，透明度，回调函数)

## jQuery事件操作

jQuery的页面加载完成之后是浏览器的内核解析完页面的标签,创建好dom对象后立即执行

原生js的页面加载完成之后，除了要等浏览器的内核解析完页面标签创建dom对象，还要等标签显示时需要的内容加载完成

$(document).ready(function(){});

$(function());

原生js的页面加载完成之后，只会执行最后一次的赋值函数

jquery的页面加载完成之后是全部把注册的function函数，依照顺序执行

### jQuery的常用事件

- click()					绑定click事件；触发每一个匹配元素的click事件 
  - 不传参数是触发，传参数是绑定
- mouseover()       鼠标移入事件
- mouseout()         鼠标移出事件
- bind()                    可以给元素一次性绑定一个或多个事件
- one()                      使用上跟bind一样，但是one方法绑定的事件只响应一次

- unbind()                与bind相反的操作，解除事件的绑定
- live()                         也是用来绑定事件，可以用来绑定选择器匹配的所有元素的事件，哪怕这个元素是后面动态创建出来的也有效

### 事件的冒泡

事件的冒泡是指，父子元素同事间厅同一个事件。当触发子元素的事件的时候，同一个事件也被传递到父元素的事件里去响应

在子元素事件函数体内，return false，可以阻止事件的冒泡传递

~~~html
<script type = "text/javascript">
	$("#di").click(function(){
        alert("div的click事件");
    });
    
    $("#sp").click(function(){
        alert("span的click事件");
        return false;
    });
</script>
<div id = "di">
    我是外层div
    <span id = "sp">我是内层span</span>
</div>
~~~

### javascript事件对象

- 原生js获取事件对象

~~~js
window.onload = function(){
    document.getElementById("areaDiv").onclick = function(event){
        console.log(event);
    }
}
~~~

- jQuery获取

~~~js
$("#areaDiv").click(function(event){
    console.log(event);
});
~~~

- 使用bind同时对多个事件绑定同一个函数

~~~js
$("areaDiv").bind("mouseover mouseout",function(event){
    if(event.type == "mouseover"){
        console.log("鼠标移入");
    }else if(event.type == "mouseout"){
        console.log("鼠标移出");
    }
});
~~~

**[ 图片跟随](./jQuery代码/图片跟随.md)**