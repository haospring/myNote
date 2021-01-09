~~~java
package com.neu.calendar;

import java.util.Calendar;

import org.junit.Test;

/**
 * 
 * @author haospring
 * @date 2020年11月12日 上午11:33:20
 * @description Calendar
 */
public class Demo01 {
	@Test
	public void method() {
		// 该类所有的数据都是以键值对形式（key=value）完成存储和显示；
		// 所有的key都是static修饰的，所以开发者想要获取具体的值可以通过类名.key找到对应的值
		Calendar c = Calendar.getInstance();
		System.out.println(c);

		// 获取年月日、时分秒
		// 注意事项：计算机中月份从0开始，0代表1月
		// 通过get()方法获取年月日、时分秒，参数格式为：Calendar.key，key是Calendar的成员属性
		System.out.println("获取年：" + c.get(Calendar.YEAR));
		System.out.println("获取月：" + (c.get(Calendar.MONDAY) + 1));
		System.out.println("获取当月几号：" + c.get(Calendar.DAY_OF_MONTH));
		System.out.println("获取小时" + c.get(Calendar.HOUR));
		System.out.println("获取分钟" + c.get(Calendar.MINUTE));
		System.out.println("获取秒数" + c.get(Calendar.SECOND));
	}
}
~~~