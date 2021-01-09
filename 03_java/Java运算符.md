# Java运算符

## 运算符

取余：%
除：/
取余的符号和被余数相同

~~~java
System.out.println(3 % 2);// 1
System.out.println(3 % -2);// 1
System.out.println(-3 % 2);// -1
System.out.println(-3 % -2);// -1
~~~

两数相除的符号和两个数都有关

~~~ java
System.out.println(3 / 2);// 1
System.out.println(3 / -2);// -1
System.out.println(-3 / 2);// -1
System.out.println(-3 / -2);// 1
~~~



### 位运算符

&、|、^、~、<<、>>、>>>
与、或、异或、取反、左移、右移、无符号右移
&：两位同时为1，结果才为1，否则结果为0
|：参加运算的两个对象只要有一个为1，其值为1
^：参加运算的两个对象，如果两个相应位相同为0，相异为1
~：对一个二进制数按位取反，即将0变1，1变0
[位运算符链接](https://www.runoob.com/w3cnote/bit-operation.html)

## 优先级

算术运算符 > 关系运算符 > 逻辑运算符 > 赋值运算符

## 流程控制

switch()括号中的数据类型只能是byte、short、int、char以及enum，jdk7可以放String