~~~java
package com.haospring.spring5;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.util.Arrays;

public class UserDaoProxy implements InvocationHandler {
    private Object obj;

    public UserDaoProxy(Object obj) {
        this.obj = obj;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        // 方法执行前
        String name = method.getName();
        System.out.println(name + "方法执行前执行，传入的参数为" + Arrays.toString(args));

        // 方法执行
        Object result = method.invoke(obj, args);

        // 方法执行后执行
        System.out.println(name + "方法执行后执行..."+result);
        return result;
    }
}
~~~

~~~java
package com.haospring.spring5;

import com.haospring.dao.UserDao;
import com.haospring.dao.impl.UserDaoImpl;

import java.lang.reflect.Proxy;

public class JDKProxy {

    public static void main(String[] args) {
        Class[] clazz = {UserDao.class};
        UserDaoImpl userDaoImpl = new UserDaoImpl();
        UserDao userDao = (UserDao) Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), clazz, new UserDaoProxy(userDaoImpl));
        int result = userDao.add(1, 2);
        System.out.println("result:" + result);

        String update = userDao.update("989");
        System.out.println(update);
    }
}
~~~

~~~java
package com.haospring.dao;

public interface UserDao {
    public int add(int a, int b);

    public String update(String id);
}
~~~

~~~java
package com.haospring.dao.impl;

import com.haospring.dao.UserDao;

public class UserDaoImpl implements UserDao {
    @Override
    public int add(int a, int b) {
        return a + b;
    }

    @Override
    public String update(String id) {
        return id;
    }
}
~~~



