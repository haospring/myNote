## Intent

### 启动 Activity 报异常

*android.content.ActivityNotFoundException: No Activity found to handle Intent { act=com.thundersoft.testnotification.activity.SecondActivity }*

~~~java
Intent intent = new Intent();
intent.setAction("com.thundersoft.testnotification.activity.SecondActivity");
startActivity(intent);
~~~

需要给 activity 设置 category 属性

~~~xml
<!-- 如果在AndroidManifest.xml 文件中设置 category 为默认，则 intent 可以不设置 category -->
<category android:name="android.intent.category.DEFAULT" />

<!-- 如果设置的 category 为自定义的，则需要在设置 intent 的 category -->
<category android:name="com.thundersoft.testnofification.mycategory" />
~~~

~~~java
intent.addCategory("com.thundersoft.testnofification.mycategory");
~~~

### 隐式启动 Service

~~~java
Intent intent = new Intent();
intent.setAction("com.thundersoft.testnotification.service.TestForegroundService");
intent.setPackage("com.thundersoft.testnotification");
startService(intent);
~~~

隐式启动 Service 必须指定包名

包名是组件的包名，不是 Service 类的包名，不是 `com.thundersoft.testnotification.service`

###　Intent 的属性

ComponentName，Action，Category，Data，Type，Extra，Flags

#### Flags: 

Intent.FLAG_ACTIVITY_CLEAR_TOP：类似于 activity 的 launchMode 为 singleTask

Intent.FLAG_ACTIVITY_SINGLE_TOP：singleTop

Intent.FLAG_ACTIVITY_NEW_TASK：singleInstance

**e.g. 依次启动A 、B、C、D，然后从 D 跳转到 B，同时希望 C、D都finish掉**

方式一：Intent 设置 Flags 属性为 Intent.FLAG_ACTIVITY_CLEAR_TOP

方式二：在 AndroidManifest.xml 中给 B 添加属性 launchMode = "singleTask"

#### ComponentName

~~~java
Intent intent = new Intent();
Intent intent = new Intent();
intent.setComponent(new ComponentName("com.thundersoft.testnotification", "com.thundersoft.testnotification.activity.SecondActivity"));

// 等价于
Intent intent = new Intent(getApplicationContext(), SecondActivity.class);
~~~

*note:* 包名指的是组件所在的包名，而不是类所在的包名，包名是 `com.thundersoft.testnotification`，而不是 `com.thundersoft.testnotification.activity`

类名需要包含类的详细路径，也就是`包名+类名`

### 参考链接

[https://www.cnblogs.com/SanguineBoy/p/9785585.html](https://www.cnblogs.com/SanguineBoy/p/9785585.html)





