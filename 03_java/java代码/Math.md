~~~java
package com.neu.math;

import org.junit.Test;

/**
 * 
 * @author haospring
 * @date 2020年11月12日 上午10:50:52
 * @description Math类中方法的使用
 */
public class Demo01 {
	@Test
	public void method() {
		// 调用属性PI
		System.out.println(Math.PI);
		// abs():绝对值
		System.out.println(Math.abs(-3));
		// ceil():向上取整
		System.out.println(Math.ceil(2.1));
		// floor():向下取整
		System.out.println(Math.floor(2.6));
		// random():随机数（伪随机数：0-1）
		System.out.println(Math.random());
		// max():最大值
		System.out.println(Math.max(3, 8));
		// min():最小值
		System.out.println(Math.min(3, 8));
		// round():四舍五入
		System.out.println(Math.round(4.4));
		System.out.println(Math.round(4.5));
        System.out.println(Math.round(-4.5));//-4，沿着数轴向右取整
        System.out.println(Math.round(-4.4));//-4
        // sqrt():开平方
		System.out.println(Math.sqrt(4));
		// pow():x的a次幂
		System.out.println(Math.pow(2, 3));
	}
}
~~~