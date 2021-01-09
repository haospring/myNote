# JDBC+Mysql项目练习

学生管理系统，面向接口编程

## 工程分层

1. dao：定义学生管理系统的接口，该接口封装了学生相关的操作方法
2. daoImpl：接口的实现层，该层定义了接口的实现类，负责完成具体学生相关的操作
3. util：定义工程中需要的工具类
4. test：定义工程中的测试类
5. entity：针对数据库表定义对应的实体类，实体类中的属性对应数据库中表的列

## 工程中各层的定义与封装

1. dao层的定义与封装

   **[StudentDao](./StudentDao.md)**

2. entity层的定义与封装

   **[Student](./Student.md)**

3. daoImpl层的定义与封装



4. test层的定义与封装

根据教师姓名，查询上过该教师的课的学生信息

~~~mysql
(select c.id from cource c,teacher t where t.id = c.teacher_id and t.name = ?) as temp

(select sc.student_id from studentcource sc,(select c.id from cource c,teacher t where t.id = c.teacher_id and t.name = ?) as temp where sc.cource_id= temp.id) as temp2

select s.* from student s,(select sc.student_id from studentcource sc,(select c.id from cource c,teacher t where t.id = c.teacher_id and t.name = ?) as temp where sc.cource_id= temp.id) as temp2 where s.id = temp2.student_id;
~~~

语文：1、3

数学：1、2、