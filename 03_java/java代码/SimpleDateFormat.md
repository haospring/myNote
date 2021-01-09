~~~java
package com.neu.simpleDateFormat;

import java.text.SimpleDateFormat;
import java.util.Date;

import org.junit.Test;

/**
 * 
 * @author haospring
 * @date 2020年11月12日 下午2:01:50
 * @description SimpleDateFormat的使用
 */
public class Demo01 {
	@Test
	public void method() throws Exception {
		// 通过不带参的SimpleDateForamt创建对象，通过对象中的format()方法，完成对
		// date日期的格式化显示
		SimpleDateFormat sdf = new SimpleDateFormat();
		Date d = new Date();

		String dateFormat = sdf.format(d);
		System.out.println(d);
		System.out.println(dateFormat);

		/*
		 * 通过带参的构造方法生成对象，构造方法可以设置日期格式； 年：yyyy 月：MM 日：dd 时：HH hh 分：mm 秒：ss
		 */
		SimpleDateFormat sdf2 = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
		String dateFormat2 = sdf2.format(d);
		System.out.println(dateFormat2);

		/*
		 * parse():该方法的作用是将字符串转换为日期
		 */
		String dateStr = "2020-12-28 12:12:12";
		SimpleDateFormat sdfDateString = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
		Date date = sdfDateString.parse(dateStr);
		System.out.println("字符串转换为date型：" + date);
	}
}

~~~