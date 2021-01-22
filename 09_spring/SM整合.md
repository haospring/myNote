## SM整合

### spring的事务控制

1. **什么是事务**

   事务：对数据库的一系列操作，用来保障同时成功或者同时失败（对数据库的数据操作），在开发中绝对不允许出现部分成功或部分失败

2. **事务的特性**

   原子性（Atomicity）：事务被视为不可分割的最小单元，要么全部提交成功，要么全部失败回滚

   一致性（Consistency）：事务执行前后都保持一致性状态。在一致性状态下，所有事务对一个数据的读取结果都是相同的

   隔离性（Isolation）：一个事务所做的修改在最终提交以前，对其它事务是不可见的

   持久性（Durability）：一旦事务提交，则其所做的修改将会永远保存到数据库中。即使系统发生崩溃，事务执行的结果也不能丢失。可以通过数据库备份和恢复来保证持久性。

   这几个特性可以简称为ACID，最重要的是隔离性

3. **并发一致性问题**

   （3.1）丢失修改：多个事务同时读取某一个数据，一个事务成功处理好了数据，被另一个数据写回原值，造成第一个事务更新丢失

   （3.2）脏读：脏读是指在一个事务处理过程里读取了另一个未提交的事务中的数据

   （3.3）不可重复读：不可重复读是指在对于数据库的某个数据，一个事务范围内多次查询却返回了不同的数据值。这是由于在查询间隔，被另一个事务修改并提交了

   （3.4）幻读（虚读）：幻读是事务非独立执行时发生的一种现象。例如，T1 读取某个范围的数据，T2在这个范围内插入新的数据，T1再次读取这个范围的数据，此时读取的结果和和第一次读取的结果不同。

4. **隔离级别**

   （4.1）读取未提交（read uncommitted）：事务中的修改，即使没有提交，对其它事务也是可见的。最低级别，任何情况都无法保证

   （4.2）读取已提交（read committed）：一个事务只能读取已经提交的事务所做的修改。换句话说，一个事务所做的修改在提交之前对其它事务是不可见的。可避免脏读的发生

   （4.3）可重复读（repeatable read）：保证在同一个事务中多次读取同样数据的结果是一样的。可避免脏读、不可重复读的发生

   （4.4）可串行化（serializable）：强制事务串行执行。可避免脏读、不可重复读、幻读的发生

   （4.5）注意事项：大多数数据库默认的事务隔离级别是read committed（oracle、sqlserver），mysql新版本默认隔离级别repeatable read

   以上四种隔离级别最高的是serializable（可串行化）级别，最低的是read uncommitted（未提交读）级别，当然级别越高，执行效率就越低。

   而在Oracle数据库中，只支持SERIALIXABLE(串行化)级别和READCOMMITTED(读已提交)这两种级别 ，其中默认的为READ COMMITTED级别。

   ![](sm%E6%95%B4%E5%90%88/%E9%9A%94%E7%A6%BB%E7%BA%A7%E5%88%AB.jpg)

   [链接：https://juejin.cn/post/6844903586300690445](https://juejin.cn/post/6844903586300690445)

5. **spring的事务管理器**

   描述：spring给开发者提供了一个事务控制的接口：PlatformTransactionManager，该接口提供了三个方法，通过这三个方法可以根据dao层使用不同的ORM框架，具体实现类如下：

   **DataSourceTransactionManager：适用于jdbc和mybatis**

   HibernateTransactionManager：适用于Hiberator

   JpaTransactionManager：适用于jpa

   JtaTransactionManager：适用于jta

   JdoTransactionManager：适用于jdo

   JmsTransactionManager：适用于jms

6. **创建表**

   数据库中创建表account，记录金额，模拟转账过程

   spring对事务的配置是通过aop完成的，aop的操作步骤如下：

   确定目标：

   编写通知（增强）

   配置切面

![](sm%E6%95%B4%E5%90%88/AccountService1.jpg)

![](sm%E6%95%B4%E5%90%88/%E4%BA%8B%E5%8A%A1%E6%8E%A7%E5%88%B6%E6%88%90%E5%8A%9F.jpg)

![](sm%E6%95%B4%E5%90%88/AccountService2.jpg)

![](sm%E6%95%B4%E5%90%88/%E4%BA%8B%E5%8A%A1%E6%8E%A7%E5%88%B6%E5%A4%B1%E8%B4%A5.jpg)

7. spring事务管理的注解开发方式

   描述：基于注解方式完成事务管理

   在需要管理事务的方法或类上面添加注解@Transactional

   在spring的配置文件中配置注解驱动的事务管理（配置事务管理器）