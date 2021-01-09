~~~java
package com.haospring.aopAnnotation;

import org.springframework.stereotype.Component;

// 被增强的类
@Component
public class User {
    public void add(){
        // int a = 1/0;
        System.out.println("add......");
    }
}

~~~

~~~java
package com.haospring.aopAnnotation;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.stereotype.Component;

// 增强的类
@Component
@Aspect
public class UserProxy {
    // 相同切入点抽取
    @Pointcut(value = "execution(* com.haospring.aopAnnotation.User.add(..))")
    public void pointDemo(){
    }

    // 前置通知
    @Before(value="pointDemo()")
    public void before(){
        System.out.println("before......");
    }

    // 后置通知
    @AfterReturning(value="pointDemo()")
    public void afterReturning(){
        System.out.println("afterReturning......");
    }

    // 异常通知
    @AfterThrowing(value="execution(* com.haospring.aopAnnotation.User.add(..))")
    public void afterThrowing(){
        System.out.println("afterThrowing......");
    }

    // 环绕通知
    @Around(value="execution(* com.haospring.aopAnnotation.User.add(..))")
    public void around(ProceedingJoinPoint joinPoint) throws Throwable {
        System.out.println("around before......");
        joinPoint.proceed();
        System.out.println("aroudn after......");
    }

    // 最终通知
    @After(value="execution(* com.haospring.aopAnnotation.User.add(..))")
    public void after(){
        System.out.println("after......");
    }
}
~~~

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">
    <!-- 开启注解扫描 -->
    <context:component-scan base-package="com.haospring.*"/>
    <!-- 开启AspectJ生成代理的对象 -->
    <aop:aspectj-autoproxy/>
</beans>
~~~

~~~java
package com.haospring.test;

import com.haospring.aopAnnotation.User;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class TestAopAnnotation {
    @Test
    public void testAopAnno(){
        ApplicationContext context = new ClassPathXmlApplicationContext("springAOP.xml");
        User user = context.getBean("user", User.class);
        user.add();
    }
}
~~~

