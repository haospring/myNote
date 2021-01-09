# JDBC

- 描述
  - Java Database Connectivity		 java数据库连接
  - jdk为开发者提供了一套通过java操作不同数据库的统一规范
  - 这个规范也就是java的jdbc编程

## JDBC使用

1. 工程的环境搭建
2. jdbc接口详细讲解
   - Driver接口，定义了操作数据库的最根本的规范，通过Class.forName()方法动态的加载到当前的程序中
   - mysql数据库驱动包实现了Driver接口，其中该驱动包提供了com.mysql.jdbc.Driver类
   - 该类中通过静态代码块创建了Driver对象，并添加到DriverManager中

- DriverManager类

  - java.sql.DriverManager
  - 用来管理多个数据库驱动，通常配合class.forName()方法使用
  - getConnection(String url,String username,String password)，通过该方法获取当前驱动对应的数据库连接
    - url：数据库访问地址，每一个数据的访问地址都不同
    - username：数据库的账号
    - password：数据库账号的密码
  - mysql的访问地址：jdbc:mysql://localhost:3306/staff
    - jdbc：连接协议
    - mysql：子协议
    - localhost：本地访问，该位置+**也可以描述访问的ip地址
    - 3306：mysql的数据库端口号
    - staff：数据库名
  - 在定义mysql访问地址同时，设定编码集合：
    - jdbc:mysql://localhost:3306/staff?characterEncoding=utf8
  - oracle的数据库连接地址
    - jdbc:mysql:thin@localhost:1521:sid

- Connection接口

  - java.sql.Connection
  - 该接口的作用封装数据库连接，接口不能直接实例化，所以通常通过DriverManager.getConnection(String url,String username,String password)类生成实例对象
  - 该接口最终要的作用是封装了对数据库各种操作的方法

  - 常用方法介绍：
    - Statement createStatement()：生成sql执行器（Statement）的实例对象
    - PreparedStatement prepareStatement（String sql）：生成sql执行器（该执行器可以防止sql的非法注入）

- Statement接口：

  - java.sql.Statement
  - 是数据库的执行器，主要用来执行sql语句，并最终完成对数据库的增、删、改、查操作功能
  - 常用方法：
    - boolean execute（String sql）：用来执行sql语句，如果执行成功则返回true，否则返回false
    - int executeUpdate（String sql）：用来执行sql语句，主要执行update、insert、delete，如果执行成功则返回大于0的数值，否则返回小于等于0的数值（返回数据库受影响的行数）
    - ResultSet executeQuery（String sql）：该方法主要用来执行select语句，并将查询到的数据自动封装到ResultSet结果集中

- ResultSet接口

  - java.sql.ResultSet
  - 该接口通过Statement中的executeQuery方法生成实力对象，并将该方法执行的查询语句返回的数据进行封装
  - 常用方法：
    - getXxx（int columnIndex）：根据指定的列的下标获取对应的数据
    - Xxx：开发者想要取值的列的java数据类型，返回值与获取列的数据类型一致
    - getXxx（String columnName）：根据指定的列名获取列所对应的值
    - Xxx：开发者想要取值的列的java数据类型，返回值与获取列的数据类型一致
    - boolean next（）：用于循环条件，判断结果集中是否有下一行数据，如果有，返回true否则false

- PreparedStatement

  - java.sql.PreparedStatement接口，是Statement的子接口
  - 该接口主要是为了防止sql注入
  - 常用方法：
    - Connection中通过prepareStatement(String sql)方法生成执行器，该方法的返回值类型为PreparedStatement

**[JDBCUtil](./JDBC代码/JDBCUtil.md)**