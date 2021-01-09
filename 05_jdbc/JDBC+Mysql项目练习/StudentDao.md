~~~java
package com.neu.dao;

import java.sql.SQLException;
import java.util.List;

import com.neu.entity.Student;

/*
 * 封装学生相关的操作方法
 */
public interface StudentDao {
	/**
	 * @Description 查询所有学生信息
	 * @return List<Student>
	 * @throws SQLException
	 */
	public abstract List<Student> findAll() throws SQLException;

	/**
	 * @Description 查询一个学生的信息
	 * @return Student
	 * @throws SQLException
	 */
	public abstract Student findOneStudent() throws SQLException;

	/**
	 * @Description 更新学生信息
	 * @param Student stu
	 * @return boolean
	 * @throws SQLException
	 */
	public abstract boolean updateStudent(Student stu) throws SQLException;

	/**
	 * @Description 根据id删除学生信息
	 * @param int id
	 * @return boolean
	 * @throws SQLException
	 */
	public abstract boolean deleteStudentById(int id) throws SQLException;

	/**
	 * @Description 删除学生信息
	 * @param Student stu
	 * @return boolean
	 * @throws SQLException
	 */
	public abstract boolean addStudent(Student stu) throws SQLException;
}
~~~

