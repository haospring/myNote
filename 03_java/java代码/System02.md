~~~java
package com.neu.system;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.io.Reader;
import java.util.Map;
import java.util.Properties;

import org.junit.Test;

/**
 * 
 * @author haospring
 * @date 2020年11月12日 上午10:12:45
 * @description 展现System的常用方法
 */
public class Demo02 {

	@Test
	public void getProperties() {
		// getProperties():获取jdk及系统的属性值
		Properties prop = System.getProperties();
		System.out.println(prop);
		System.out.println("---------------------------------");

		// clearProperty(String key):清除jvm获取到的指定key对应的数据
		String clearProperty = System.clearProperty("sun.desktop");
		System.out.println(clearProperty);
		System.out.println(prop);
		System.out.println("---------------------------------");

		// getenv():获取系统的环境变量
		Map<String, String> map = System.getenv();
		System.out.println("系统的环境变量：" + map);
		System.out.println("---------------------------------");

		// currentTimeMillis():获取当前系统的时间，单位为毫秒
		long timeMillis = System.currentTimeMillis();
		System.out.println("获取系统时间，转换为毫秒显示：" + timeMillis);
		System.out.println("---------------------------------");

		// exit(int a):终止jvm运行
		// System.exit(0);
		// System.out.println("看不见我！！！");

		// gc():运行垃圾回收器，告诉jvm运行垃圾回收器开始回收垃圾（但是不一定马上进行）
		System.gc();
	}

	@Test
	public void method() {
		// 创建Properties对象
		Properties prop = new Properties();
		File file = new File("D:\\sts-4.5.1.RELEASE\\workspace\\javaproject_08_20201112\\src\\com\\neu\\system\\information.properties");
		// 采用输入流读取配置文件
		try {
			Reader reader = new BufferedReader(new FileReader(file));
			prop.load(reader);
			String name = prop.getProperty("name");
			System.out.println(name);
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}

	}
}
~~~