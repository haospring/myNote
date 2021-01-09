~~~java
package com.neu.integer;

import org.junit.Test;

/**
 * 
 * @author haospring
 * @date 2020年11月12日 下午2:53:02
 * @description int对应包装类Integer的使用
 */
public class Demo01 {
	@SuppressWarnings("deprecation")
	@Test
	public void method() {
		int x = 123;
		// 将int类型变量转换为对应的包装类Integer
		Integer i = new Integer(x);// 过时，不推荐使用
		System.out.println(i);

		String str = "234";
		Integer i2 = new Integer(str);
		System.out.println(i2);

		Integer i3 = Integer.valueOf(x);
		System.out.println(i3);

		Integer i4 = Integer.valueOf(str);
		System.out.println(i4);

		// 将包装类中的数值转换为基本数据类型
		Integer i5 = Integer.valueOf(345);
		int a = i5.intValue();
		System.out.println(a);

		// 将Double数据3.14转换为double3.14
		Double d = Double.valueOf(3.14);
		double d2 = d.doubleValue();
		System.out.println(d2);

		// Integer转换为int，自动拆装箱（jdk5之后）
		Integer i6 = 12;// 自动装箱
		int a2 = i6;// 自动拆箱
		System.out.println(a2);
	}
}
~~~