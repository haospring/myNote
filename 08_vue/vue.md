# vue

## 基础应用

### 介绍

1. vue的底层是js，使用vue的开发者，只需要关注视图层开发即可，可以真正的实现前后端分离；所以也称为渐进式的开发框架。

   渐进式：用最少的代码完成最多的功能；

   前端主流框架：

   （1）Angular.js（Google），提供了数据模板，能实现脚本与数据的双向访问；

   （2）React.js，它的封装性更强，主要是组件化开发和虚拟化的dom；

   （3）Vue.js，借鉴了以上两种框架的优点，并采用MVVM的思想，构建了新的渐进式的开发框架；

![基本格式](vue%E5%9B%BE%E7%89%87/%E5%9F%BA%E6%9C%AC%E6%A0%BC%E5%BC%8F.jpg)

2. MVVM思想

   MVVM：Model View ViewModel三层

   - Model：指代的是vue中data声明的参数及对应的值（将参数对应的值提供给绑定的控件--渲染到视图层中的数据）；

   - View：指代的是el绑定的元素节点（具体的标签），注意事项view不是指代的整个的html，它所关注的只是el所描述的这一部分；
   - ViewModel：指代的是vue的调度器，通常开发者命名为vm，在代码中通过new Vue({});来生成vm调度器对象，调度器作用是控制model（data）与view（el）的关系；vm调度器使用的是虚拟的dom

   什么是dom？

   - 在js中，所有的标签（节点）都封装在dom树中，每一次都需要对dom进行遍历，目的是为了找到节点（譬如：getElementById），一旦节点的数据发生变化，就需要重新刷新dom树，所以传统的dom效率低
   - 虚拟dom：vue采用的是虚拟dom，克隆了真实的dom，通常在开发中虚拟dom称为v-dom

3. vue中常用的指令和语法

   （1）v-text属性：替换对应标签的文本数据

 ![v-text](vue%E5%9B%BE%E7%89%87/v-text.jpg)

​		说明：v-text是替换掉文本信息，所以上面代码中“这是v-text的使用”不会被显示，替换为“张三”，而差值表达式不会替换文本信息，所以上面代码会显示“差值表达式的值：张三”。 

​	（2）v-html属性：替换对应标签的文本数据

 ![v-html](vue%E5%9B%BE%E7%89%87/v-html.jpg)

​	v-html可以解析html标签（标记），上述例子中的<h1>是可解析的，v-text 不能解析html标签

​	（3）v-bind属性：强制绑定html标签属性，目的是为了让属性强制接收model（data）中的数据

 ![v-bind](vue%E5%9B%BE%E7%89%87/v-bind.jpg)

​	v-bind：绑定的标签属性也可以省略为：+绑定的标签属性

​	v-bind绑定的属性如果在双引号中出现单引号，意味着单引号中的内容原样输出，如果没有单引号，则双引号所描述的就是model（data）中参数对应的值

​	（4）v-model属性：声明数据，数据可以与标签（控件||元素）实现双向绑定，双向绑定实际上就是双向的数据交互，只能用于input、select、textarea

 ![v-model](vue%E5%9B%BE%E7%89%87/v-model.jpg)

​	v-model：是完成数据双向绑定和交互的（标签<=>data），标签引用data则数据不发生改变，如果完成双向绑定，页面标签引用data中的数据可以随时变化，标签中的数据变了，data中的数据也会变化

- text 和 textarea 元素使用 `value` property 和 `input` 事件；
- checkbox 和 radio 使用 `checked` property 和 `change` 事件；
- select 字段将 `value` 作为 prop 并将 `change` 作为事件。

​	练习1：单选框

 ![exam_v-model](vue%E5%9B%BE%E7%89%87/exam_v-model.jpg)

​	练习2：复选框

 ![exam02_v-model.jpg](vue%E5%9B%BE%E7%89%87/exam02_v-model.jpg)

​	练习：下拉框

 ![下拉框](vue%E5%9B%BE%E7%89%87/%E4%B8%8B%E6%8B%89%E6%A1%86.jpg)

​	（5）v-show与v-if

​	v-show：通过该属性控制display，来完成标签是否显示，如果值为true，则显示，否则隐藏

​	v-if：通过该属性，可以对标签进行删除操作，如果值为true，保留显示，否则删除

​	（6）v-else-if

​	声明boolean类型的数据，等价于java中的else if的使用；使用过程中注意事项：v-if和v-else-if一起使用时，二者之间不能存在其他的数据，必须连着写

 ![省市区三级联动](vue%E5%9B%BE%E7%89%87/%E7%9C%81%E5%B8%82%E5%8C%BA%E4%B8%89%E7%BA%A7%E8%81%94%E5%8A%A8.jpg)

​	总结：v-if、v-else-if、v-else，由它们定义的程序在执行时按照从上而下的顺序进行执行，一旦满足条件则后续内容不执行，条件满足时该属性执行的是标签的删除操作；等价于java中的if else if else

（7）v-for属性：相当于for循环（等价于foreach），可以用来循环简单的数组、对象、或者是指定范围的数字

方式一：v-for = "接收数组元素的变量名 in 数组名"；

方式二：v-for = "（接收数组元素的变量名，接收数组索引） in 数组名"；

~~~html
<div id="box10">
    <!-- 两种方式完成循环 -->
    <ul>
        第一种循环方式，使用插值表达式：<li v-for="name in names">{{name}}</li>
        第一种循环方式，使用v-text：<li v-for="name in names" v-text="name"></li>
        第二种循环方式，带有数组的下标：<li v-for="(name,index) in names">数组元素：{{name}}
        - 数组下标：{{index}}</li>
    </ul>
</div>
</body>
<script>
    var vm = new Vue({
        el: "#box10",
        data: {
            names: ["三", "四", "五"]
        }
    });
</script>
~~~

方式三：循环对象数组：v-for = "(用来接收对象的变量，索引) in 数组名"；

~~~html
<table border="1" cellspacing="0" cellpadding="0">
    <tr>
        <th>序号</th>
        <th>学生编号</th>
        <th>学生姓名</th>
        <th>学生年龄</th>
    </tr>
    <tr v-for="(stu,i) in students">
        <td>{{i+1}}</td>
        <td v-text="">{{stu.id}}</td>
        <td v-text="">{{stu.name}}</td>
        <td v-text="">{{stu.age}}</td>
    </tr>
</table>
<table border="1" cellspacing="0" cellpadding="0">
    <tr>
        <th>序号</th>
        <th>教师编号</th>
        <th>教师姓名</th>
        <th>教师年龄</th>
    </tr>
    <tr v-for="(tec,i2) in teachers">
        <td>{{i2+1}}</td>
        <td>{{tec.id}}</td>
        <td>{{tec.name}}</td>
        <td>{{tec.age}}</td>
    </tr>
</table>
</div>
</body>
<script>
    var vm = new Vue({
        el: "#box11",
        data: {
            students: [{id: 1001,name: "tom",age: 18},
                       {id: 1002,name: "jerry",age: 18},
                       {id: 1003,name: "lily",age: 19}
                      ],
            teachers: [{id: 2231,name: "老明",age: 38},
                       {id: 2232,name: "老王",age: 40},
                       {id: 2233,name: "老刘",age: 45
                       }
                      ]
        }
    });
</script>
~~~

方式四：循环对象：v-for = "(自定义的变量接收值，自定义变量接收key，自定义变量接收索引) in 对象名"

~~~html
<div id="box12">
    <p v-for="(value,key,i) in teacher">
        老师的属性值：{{value}}<br />
        老师的属性：{{key}}<br />
        老师的索引：{{i}}<br />
    </p>
</div>
</body>
<script>
    var vm = new Vue({
        el: "#box12",
        data: {
            teacher: {
                id: 12,
                name: "zhou",
                age: 56
            }
        }
    });
</script>
~~~

方式五：指定数字范围的循环

~~~html
<div v-for="count in 5">
    循环的数字为：{{count}}
</div>
~~~

指定范围的数字循环只能从1开始，步长为1（每次循环值的增长）

（8）v-on属性：绑定js事件，该属性可以简化为@符号写法

~~~html
<div id="box15">
    输入值1：<input type="text" v-model.number="num1" />
    <select v-model="operator">
        <option value="1">+</option>
        <option value="2">-</option>
        <option value="3">*</option>
        <option value="4">/</option>
    </select>

    输入值2：<input type="text" v-model.number="num2" />
    结果：<input type="text" :value="num3" />
    <input type="button" value="计算" @click="calculation" />

</div>
</body>
<script>
    var vm = new Vue({
        el: "#box15",
        data: {
            num1: "",
            num2: "",
            num3: "",
            operator: 1
        },
        methods: {
            calculation: function() {
                if (this.operator == 1) {
                    this.num3 = this.num1 + this.num2
                } else if (this.operator == 2) {
                    this.num3 = this.num1 - this.num2
                } else if (this.operator == 3) {
                    this.num3 = this.num1 * this.num2
                } else {
                    if (this.num2 != 0) {
                        this.num3 = this.num1 / this.num2
                    } else {
                        alert("除数不能为0");
                    }
                }

            }
        }
    });
</script>
~~~

~~~html
<body>
    <div id="box16">
        <input type="text" v-model="bookAdd" />
        <input type="button" @click="add" value="添加" /><br />
        <input type="text" v-model="bookRemove" />
        <input type="button" @click="remove" value="删除" /><br />

        <ul>
            <li v-for="bk in books" v-text="bk"></li>
        </ul>
    </div>
</body>
<script>
    var vm = new Vue({
        el: "#box16",
        data: {
            bookAdd: "",
            bookRemove: "",
            books: ["九阴白骨爪", "九阳神功", "蛤蟆功"]
        },
        methods: {
            add: function() {
                if (this.bookAdd != "") {
                    this.books.push(this.bookAdd);
                }
            },
            remove: function() {
                for (var i in this.books) {
                    if (this.bookRemove == this.books[i]) {
                        this.books.splice(i,1);
                    }
                }
            }
        }
    });
</script>
~~~

[学生增删练习](代码/学生增删练习.md)

（9）vue如何绑定css属性（class）

开发中可以通过class属性绑定对应的标签（元素||控件||节点元素），如果vue想要绑定样式，可以通过v-bind绑定class属性值

方式一：直接声明字符串完成样式引用

描述：声明一个字符串数字，可以用来绑定class中所描述的数据，在使用时不能出现传统的空格定义方式；必须在双引号中添加单引号进行引用

[链接](代码/绑定css属性的方式.md)

（10）直接以数组的方式进行变量声明
[数组的方式](代码/数组的方式.md)

（11）声明对象：对象的key表示字符串数据，对应的值使用boolean类型的值，当值为true字符串生效

~~~html
<body>
    <div id="box05">
        <!-- <div :class="{'widthStyle':true,'heightStyle':false,'colorStyle':true}">
		通过声明对象的方式完成key的设定，如果为true则样式生效
		</div> -->
        <div :class="styles">
            通过声明对象的方式完成key的设定，如果为true则样式生效
        </div>
    </div>
</body>
<script>
    var vm = new Vue({
        el: "#box05",
        data: {
            styles:{'widthStyle':true,'heightStyle':false,'colorStyle':true}
        }
    });
</script>
~~~

（12）声明对象数组

[声明对象数组](代码/声明对象数组.md)

[复选框更改颜色](代码/复选框更改颜色.md)

（13）vue绑定style属性

方式一：直接声明对象

方式二：直接声明对象参数

方式三：声明对象数组

[style](代码/style.md)

4. vue的事件修饰符

   （1）事件修饰符是事件触发后，可以控制事件触发的机制或者流程的一种特殊的属性

   语法格式：@事件.修饰符

   （2）stop：阻止事件冒泡的修饰符

   事件冒泡：当我们在触发子标签（元素）时，会间接触发他的父元素所绑定的元素

   （3）prevent：阻止事件默认行为的发生

   （4）capture：改变事件的触发机制
   
   （5）self：只会对对应的元素进行控制（对添加属性事件不会受到事件冒泡的影响）
   
   （6）once：它所修饰的事件只在第一次触发时生效
   
   总结：事件修饰符是用来改变调用顺序的，所有的事件修饰符可以一起使用，使用的顺序没有要求
   
   [v_self](代码/v_self.md)
   
   [v_once](代码/v_once.md)
   
5. 键盘按键修饰符

   （1）按键修饰符与事件修饰符有些类似，都是通过@事件.案件修饰符来完成的；不同在于按键修饰符只能在键盘事件中使用；eg. keyup按键抬起事件、keydown按键按下时触发的事件；

   vue中常用的按键修饰符：

   @事件.enter：回车被按下时触发

   @事件.tab：tab被按下时触发

   @事件.delete：delete被按下时触发

   @事件.esc：esc按下时触发

   @事件.up：向上箭头被按下时触发

   @事件.down：向下箭头被按下时触发

   @事件.left：向左箭头被按下时触发

   @事件.right：向右箭头被按下时触发

   （2）自定义按键修饰符

   描述：指定键盘码（keyCode）：keyCode属性代表键盘中的键盘码，每一个按键都有唯一的一个整数值，所以可以通过keyCode的数值确定用户按下的是哪一个按键

   语法格式：@事件.keyCode = "函数"

   ~~~html
   <div id="box03">
       用户名：<input type="text" v-model="name" @keyup.65="add" /><br />
       <input type="button" value="添加" @click="add" />
       <ul>
           <li v-for="stu in students" v-text="'姓名:'+stu.name"></li>
       </ul>
   </div>
   ~~~

   [自定义键盘修饰属性](代码/自定义键盘修饰属性.md)

   自定义的属性名不能使用驼峰命名（不能出现大写字母），如果开发者定义的属性名为单一的字母，则该字母可以大写

6. vue鼠标修饰符&vue的计算属性

   （1）鼠标修饰符

   描述：鼠标修饰符只能绑定鼠标事件；e.g.click、dbclick、onmousedown等

   语法格式：

   @鼠标事件.left：鼠标左键按下时触发

   @鼠标事件.right：鼠标右键按下时触发

   ~~~html
   <input type="button" value="添加" @click.right="add" />
   <input type="button" value="添加" @dblclick.left="add"/>
   ~~~

   （2）计算属性

   描述：在new Vue实例中，通过引用vue提供的computed声明计算属性，它的内部可以声明函数，函数可以绑定视图中的参数，可以通过函数的return（返回值）渲染到视图层中指定的位置

   ~~~html
   <input type="text" v-model="num1" />
   <input type="text" v-model="num2" />
   <input type="text" :value="result"/>
   <script>
       var vm = new Vue({
           el: "#box06",
           data: {
               num1: 0,
               num2: 0
           },
           computed: {
               result() {
                   return parseInt(this.num1) + parseInt(this.num2);
               }
           }
       });
   </script>
   ~~~

   总结：

   计算属性可以封装复杂代码，通过自定义的函数可以让开发者除了完成计算，还可以封装流程代码

   计算属性完成的每一个操作都会存储到缓存里，如果计算操作的数值没有变化，则不会重新加载运算代码，而是直接从缓存找到相同的计算结果进行输出显示，提高了页面的加载效率

7. vue中的过滤器属性的使用

   （1）vue中的过滤器是开发者自定义的过滤器，可以通过过滤器来格式化一些文本信息，过滤器通过filters属性进行声明

   （2）带有参数的过滤器

   ~~~html
   <input type="text" :value="name|filterName('男')" />
   <script>
       data: {
           name: "隔壁老王"
       },
       filters: {
          filterName(obj, param) {
              console.log("过滤函数被执行，第一个参数值：" + obj);
              console.log("过滤函数被执行，第二个参数值：" + param);
              return "姓名：" + obj + "，性别：" + param;
          }
       }
   </script>
   ~~~

   （3）全局过滤器的使用

   通过filters属性定义的过滤器只能在当前的vue实例中（局部的过滤器），如果其他vue实例想要使用，无法找到该过滤器函数，所以开发者需要定义全局过滤器，该全局过滤器可以共享给其他vue实例

   [全局过滤器](代码/全局过滤器.md)

8. vue的自定义属性

   描述：vue自定义属性（钩子函数），在实例vue时，通过directives属性声明开发者自定义的属性，可以将自定义的属性绑定到指定的函数中

   [vue自定义指令](代码/vue自定义指令.md)
   
9. 自定义指令中常用的钩子函数

   在开发者自定义封装指令（属性）中，可以使用5个钩子函数，每一个钩子函数代表触发的时机都是不一样的，钩子函数函数名是固定的（vue提供的），对于开发者而言直接使用即可

   （1）bind：第一次执行，并且只执行一次，在标签（节点||控件）没有渲染到真实dom树的时候执行，所以无法通过el获取到标签的父节点和子节点对象；

   （2）inserted：节点渲染到真实dom树，然后执行当前函数，所以开发者可以在当前的函数中获取到父节点和子节点的对象

   （3）update：当绑定的指令（自定义的属性）发生变化（虚拟dom中的指令），还没有渲染到真实dom；

   （4）componentUpdated：绑定指令发生变化时，已经渲染到真实dom树后才执行

   （5）unbind：当前绑定被销毁时执行

   ~~~html
   <script>
       var vm = new Vue({
           el: "#box01",
           data: {
               color: "green"
           },
           directives: {
               color: {
                   bind(el, binding) {
                       console.log("bind函数被执行");
                       console.log("el的id值:" + el.id);
                       console.log("div父节点的对象：" + el.parentNode);
                   },
                   inserted(el, binding) {
                       console.log("inserted函数被执行");
                       console.log("div的id值：" + el.id);
                       console.log("div父节点对象：" + el.parentNode);
                   },
                   update(el, binding) {
                       console.log("update函数被执行");
                       console.log("颜色：" + binding.value);
                       el.style.backgroundColor = binding.value;
                   },
                   componentUpdated(el, binding) {
                       console.log("componentUpdated函数被执行");
                   },
                   unbind(el, binding) {
                       console.log("unbind被执行");
                   }
               }
   
           }
       });
   </script>
   ~~~

## 10. vue的生命周期

vue的生命周期通过钩子函数进行诠释，介绍四个部分：

（1）new Vue()：实例化Vue，初始化vue相关的参数，更新虚拟dom对象属性，在这个过程中可以分为两步：

（1.1）beforeCreate钩子函数：在实例化完毕之后，参数初始化之前（无法获取data、methods等）

（1.2）created钩子函数：构建完毕之后，初始化参数完毕之后执行（可以获取data、methods等）

（2）挂载：将虚拟dom中的信息挂载到真实dom树中（将虚拟dom中的数据更新到真实dom树中），此过程包含两个钩子函数：

（2.1）beforeMount：根据el绑定视图，加载真实dom，并渲染为虚拟dom，是在挂载到真实dom之前执行（真实dom中插值表达式获取不到值）

（2.2）mounted：根据el绑定视图，将虚拟dom挂载到真实dom后执行（真实dom中的差值表达式可以获取到值）

（3）更新：当真实dom树中节点的数据发生变化时，重新操作虚拟dom对象，并重新挂载真实dom；具备两个钩子函数：

（3.1）beforeUpdate：当数据变化时，是在虚拟dom挂载到真实dom之前执行

（3.2）updated：当数据变化时，是在虚拟dom挂载到真实dom之后执行

（4）销毁：vue实例被销毁；具备两个钩子函数

（4.1）beforeDestroy：在Vue实例被销毁之前执行

（4.2）destroyed：在Vue实例被销毁之后执行

[vue的生命周期](代码/vue的生命周期.md)

## Vue的http

### 全局语法格式

Vue.http.get('url',[options]).then(successCallBack,errorCallBack);

url：访问地址

options：用来完成业务处理，功能代码封装；譬如：地址绑定的参数

then(successCallBack，errorCallBack)：成功的回调函数和失败的回调函数

### 局部语法格式

所有的代码都需要封装到new Vue()中

this.$http.get('url',[options]).then(successCallBack,errorCallBack);

[局部语法格式](代码/局部语法格式.md)



