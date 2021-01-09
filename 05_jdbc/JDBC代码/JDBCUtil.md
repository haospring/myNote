~~~java
package com.neu.utils;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

/**
 * 
 * @author haospring
 * @date 2020年11月25日 上午10:01:36
 * @description 工具类：（1）获取Connection对象（2）释放资源
 */
public class JDBCUtil {
	private static String url = "jdbc:mysql://localhost:3306/staff?characterEncoding=utf8";
	private static String username = "root";
	private static String password = "mysql";
	private static String driver = "com.mysql.jdbc.Driver";
	private static Connection conn = null;

	static {
		try {
			Class.forName(driver);
			conn = DriverManager.getConnection(url, username, password);
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		}

	}

	public static Connection getConn() {
		return conn;
	}

	public static void close(Connection conn, Statement st, ResultSet rs) throws SQLException {
		if (conn != null) {
			conn.close();
		}
		if (st != null) {
			st.close();
		}
		if (rs != null) {
			rs.close();
		}
	}

}
~~~

