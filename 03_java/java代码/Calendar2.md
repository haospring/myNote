~~~java
package com.neu.calendar;

import java.util.Calendar;

import org.junit.Test;

/**
 * 
 * @author haospring
 * @date 2020年11月12日 下午1:41:23
 * @description Calendar方法的使用
 */
public class Demo02 {
	@Test
	public void test() {
		// set(int key,int value)：第一个参数属于想要修改的key
		// 第二个参数输入要修改的值
		Calendar c = Calendar.getInstance();
		c.set(Calendar.YEAR, 2021);
		System.out.println(c.get(Calendar.YEAR));

		c.set(2000, 1, 20);
		System.out.println(c.get(Calendar.YEAR));
		System.out.println(c.get(Calendar.MONDAY));
		System.out.println(c.get(Calendar.DATE));

		// add(int key,int value)：在原有的事件上进行增加和减少
		// 第二个参数如果是正数代表增加，反之减少
		c.add(Calendar.MONDAY, 10);
		System.out.println(c.get(Calendar.MONDAY));
	}
}
~~~