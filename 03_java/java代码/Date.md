~~~java
package com.neu.date;

import java.util.Date;

import org.junit.Test;

/**
 * 
 * @author haospring
 * @date 2020年11月12日 上午11:09:29
 * @description java.util.Date的使用
 */
public class Demo01 {
	@Test
	public void method() {
		// 创建Date对象，通过该对象显示当前系统时间：
		// Date的系统时间显示单位与System.currentTimeMillis的实践单位是为一样都是毫秒
		Date date = new Date();
		System.out.println("Date显示的系统时间为：" + date);
		long millis = date.getTime();
		System.out.println("Date类的getTime()方法显示的时间为：" + millis);
		System.out.println("System方法显示的系统时间为：" + System.currentTimeMillis());
		Date date2 = new Date(1605151063366L);
		System.out.println(date2);
	}
}
~~~