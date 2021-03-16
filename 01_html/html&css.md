# html&css第一章

## body属性

bgcolor = "red"：背景颜色

text = "yellow"：字体颜色

## 常用标签

~~~html
<!-- 文本或图片居中 -->
<center>居中</center>
<!-- 标题标签 -->
<h1>一级标题</h1>
<h6>六级标题</h6>
<!-- 段落标签 -->
<p>段落标签</p>
<!-- 换行 -->
<br/>
<!-- 水平线 color属性 -->
<hr color = "black"/>
<!-- 图片标签 -->
<!-- title属性，鼠标悬停时显示的文字 -->
<img src = "imgs/top.png" title = "前端技术" alt="图片加载失败"/>
<!-- 超链接 -->
<!-- 超链接去下划线text-decoration : none; -->
<a href = "https://www.baidu.com" target = "_blank">百度</a>
<em>一般强调，斜体</em>
<strong>特殊强调，黑体</strong>
&nbsp;空格
&lt;小于
&gt;大于
&amp;and符号
&quot;双引号
&yen;人民币
<!-- 列表 无序列表 有序列表 -->
<!-- type属性disc实心圆 circle空心圆 square实心方块 none不显示-->
<!-- css样式list-style:none;无序列表前的修饰去掉 -->
<!-- 代码生成公式 ul>li*3 >代表子标记 -->
<ul type = "disc">
    <li>HTML</li>
	<li>CSS</li>
	<li>JAVASCRIPT</li>
</ul>
<!-- type属性 1 a A i I -->
<ol type="I">
	<li>HTML</li>
	<li>CSS</li>
	<li>JAVASCRIPT</li>
</ol>
<!-- 代码生成公式 dl>(dt+dd)*3 +代表兄弟关系-->
<dl>
	<dt>html</dt>
	<dd>超文本标记语言</dd>
	<dt>css</dt>
	<dd>层叠样式表</dd>
	<dt>JavaScript</dt>
	<dd>动态脚本语言</dd>
</dl>
<!-- dl:definition list -->
<!-- dt:definition term -->
<!-- dd:definition description -->
~~~

# html&css第二章

## css基本语法

### css选择器

#### 基本选择器

1. 标签选择器

   标签名{}

2. 类选择器

   .类名{}

3. id选择器

   #id{}

   优先级：id > 类 > 标签

#### 高级选择器

1. 后代选择器

   - body p{}

   - body>p{} 子选择器：只有一代
   - .p2 + p{} 相邻兄弟选择器：只有一个，相邻向下
   - .p2 ~ p{} 通用选择器:当前标签向下所有兄弟元素

2. 交集选择器，后面只能是类或者id

   h1.hao{}

3. 并集选择器

   h1,.xyz,#spring{}

### css引入方式

1. 行内样式（不推荐）

   ~~~ html
   <p style="color: red;font-size: 30px;">
   ~~~

2. 内部样式（简便）

   ~~~ html
   <style type="text/css">
   	.in{
   		color: purple;
   		font-size: 30px;
   	}
   </style>
   ~~~

3. 外部样式（推荐）

   ~~~html
   <link rel="stylesheet" type="text/css" href="css/外部样式.css"/>
   ~~~

### css的继承特性

子标签继承父标签的样式，子标签的样式改变不会影响父标签的样式

#### css的层叠特性

~~~html
<!-- 层叠指的是多段样式代码在一个标签生效 -->
<style type = "text/css">
	.a{
		color: antiquewhite;
	}	
	.b{
		font-size: 50px;
	}
</style>
<h1 class="a b">一级标题</h1>
~~~

### css优先级

1. 不同选择器：id  > 类 > 标签
2. 相同选择器：代码的前后顺序
3. 不同的引入方式比较：行内 > 内部 > 外部

# html&css第三章

## css字体样式

font-family：设置字体类型

~~~html
font-family:"黑体";
~~~

font-size：设置字体大小，默认16px

~~~ html
font-size: 20px;
~~~

font-style：设置字体风格

~~~html
<!-- normal正常，italio斜体， -->
font-style: normal;
~~~

font-weight：设置字体的粗细

~~~html
<!-- 默认为400 -->
font-weight: 900;
~~~

## 文本样式

color：设置文本颜色

~~~ html
color:red;
color: #000000;
~~~

text-align：设置元素水平对齐方式

~~~html
text-align: center;
<!-- 文本两端对齐 -->
text-align:justify;
~~~

text-indent：设置首行文本的缩进

~~~ html
text-indent: 20px;
~~~

line-height：设置文本的行高

~~~html
<!-- 默认18px -->
line-height: 30px;
~~~

text-decoration：设置文本的装饰

~~~html
none:默认值，定义的标准文本
overline：上划线
underline：下划线
line-through：删除线
<!-- 超链接去下划线text-decoration : none; -->
~~~

text-shadow：设置文本的阴影

~~~html
h-shadow：水平阴影的位置（horizontal）
v-shadow：垂直阴影的位置（vertical）
blur：阴影距离
color：阴影颜色
text-shadow: 5px 3px 3px #674c90;
~~~

# 盒子模型

- margin 外边距 属性：上，右，下，左
- padding 内边距 属性：上，右，下，左
- border 边框，属性：粗细，样式（solid实线），颜色
  - border-radius 属性：左上，右上，右下，左下，等于宽度和高度则是圆
- background-image: linear-gradient(115deg,#008000 0%,#6248FF 50%,#FF0000 100%); 背景颜色渐变轴为115度，三种颜色渐变，高度分别为0% 50% 100%
- background-repeat 背景平铺样式
  - repeat 默认。背景图像将在垂直方向和水平方向重复。
  - repeat-x 背景图像将在水平方向重复。
  - repeat-y 背景图像将在垂直方向重复。
  - no-repeat 背景图像将仅显示一次。
  - inherit 规定应该从父元素继承 background-repeat 属性的设置。
- 块级元素：独占一行，如h1~h6,p div ,列表
- 行内元素：不独占一行，span,a,img,strong,button…
  - display属性可修改元素类型
    - block 块元素
    - inline 行内元素
    - inline-block 是块元素，但是可以内联，在一行
    - none 隐藏
- 行内块元素

# 表格和表单

## 表格

~~~html
<!-- 表格单元格合并思路 -->
<!-- 1.完整的表格 -->
<!-- 2.删掉多余的列 -->
<!-- 3.rowspan跨行显示，从上至下 colspan跨列显示，从左至右 -->

<!-- align放在table里是设置表格相对于页面的位置 -->
<!-- border设置边框 -->
<!-- cellspacing设置单元格之间的距离，为0时是距离为0，不是完全重合 -->
<!-- css样式border-collapse:collapse;单元格边框合并 -->
<table align = "center" border = "1" cellspacing = "0" width = "300" height = "300">
    <caption>表格标题</caption>
    <tr>
    	<th>表头，黑体加粗，居中</th>
        <th></th>
        <th></th>
    </tr>
    <tr>
    	<td></td>
        <td></td>
        <td></td>
    </tr>
</table>
~~~

## 表单

需要用户输入或选择的信息，都要在表单里，可以将表单和表格配合使用，实现表单的整齐

- 表单提交时，数据没有发送给服务器的三种情况
  - 表单项没有name属性值
  - 单选、复选（下拉列表中的option标签）都需要添加value属性，以便提交到服务器
  - 表单项不在提交的form标签中
- get请求的特点
  - 浏览器地址栏中的地址是：action[+?+请求参数]
  - 不安全
  - 有数据长度的限制
- post请求的特点
  - 浏览器地址栏中只有action属性值
  - 相对于get请求更安全
  - 理论上没有数据长度的限制

~~~html
<!-- action属性设置提交的服务器地址 -->
<!-- method属性设置提交的方式get（默认值）或post -->
<form action = "#" method = "get"></form>
~~~

1. 文本框

   ~~~html
   <!-- type:类型 value：默认值 maxlength：最大输入字符数 placeholder:输入提示-->
   <input type = "text" value = "默认值" maxlength = "5" placeholder = "请输入名字">
   <!-- readonly属性，只读 -->
   <input type="text" value="只读,不可更改" readonly="readonly"/>
   <!-- disabled属性，禁用，无法使用 -->
   <input type="text" disabled="disabled" />
   ~~~

2. 密码框

   ~~~html
   <!-- 当label标签的for属性和文本框的id属性相同时，聚焦 -->
   <label for="pw">密码框:</label>
   <input type="password" id = "pw"/>
   ~~~


3. 单选按钮

   必须设置value值

   ~~~html
   <!-- 代码生成公式[属性=值] -->
   <!-- name属性相同时才能互斥 -->
   <!-- checked属性，默认选中 -->
   <input type="radio" name="gender" checked="checked">男
   <input type="radio" name="gender">女
   ~~~

4. 复选框

   必须设置value值

   ~~~html
   <input type="checkbox" name="kinds" />美妆
   <input type="checkbox" name="kinds" />男装
   <input type="checkbox" name="kinds" />女装
   <input type="checkbox" name="kinds" />鞋狗
   <input type="checkbox" name="kinds" />潮玩
   ~~~

5. 下拉列表 选择框

   ~~~html
   <!-- selected属性，默认选择 -->
   <!-- select标签的multiple = "multiple"可以设置多选 -->
   <select multiple="multiple">
   	<option value ="1">辽宁</option>
   	<option value ="2" selected="selected">黑龙江</option>
   	<option value ="2">吉林</option>
   </select>
   ~~~

6. 文本域

   设置文本域的框大小不可拖动，需要加resize：none样式

   ~~~html
   <textarea rows="5" cols="20" resize="none">我是文本域的默认值</textarea>
   ~~~

7. 文件上传

   ~~~html
   <input type="file" />
   ~~~

8. 按钮

   ~~~html
   <button type="button">普通按钮</button>
   <button type="submit">提交按钮</button>
   <button type="reset">重置按钮</button>
   <input type = "submit" value = "提交" />
   <input type = "reset" value = "重置" />
   <input type = "button" value = "按钮" />
   ~~~
   
9. 隐藏域

   ~~~html
   <!-- 当我们要发送某些信息，而这些信息，不需要用户参与，就可以使用隐藏域（提交的时候同时发送给服务器） -->
   <input type = "hidden" name = "a" value = "abc" />
   ~~~

# 浮动

# 定位

## position属性

~~~html
static：默认值、没有定位

<!-- 不脱离标准流，原有的位置不会被其后的元素占用；移动参考点是标准流中的位置 -->
relative：相对定位

<!-- 1.参考点：浏览器窗口；设置了定位属性的父标记 2.脱离标准流，原来的位置释放,到达了绝对定位平面-->
absolute：绝对定位

<!-- 1.参考点是浏览器窗口 2.脱离标准流，原来的位置释放 -->
fixed：固定定位
~~~

- 图层
  - z-index 最小为0，越大越在前面
  - opacity 0~1，透明度，越小越透明

# iframe

~~~html
<!-- 将a标签的target属性值设置为iframe的name属性值，可直接在iframe中跳转 -->
<iframe src = "test.html" width = "500" height = "500" name = "abc"></iframe>
<a href = "https://www.baidu.com" target = "abc">百度</a>
~~~

