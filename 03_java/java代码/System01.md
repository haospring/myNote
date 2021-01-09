~~~java
package com.neu.system;

import java.io.PrintStream;

import org.junit.Test;

/**
 * 
 * @author haospring
 * @date 2020年11月12日 上午10:07:17
 * @description 展示System的使用
 */
public class Demo01 {
	@Test
	public void method() {
		PrintStream ps = System.out;
		ps.println("成功输出");
		System.out.println("成功输出");
		
		PrintStream ps1 = System.err;
		ps1.println("成功输出");
		System.err.println("成功输出");
	}
}
~~~