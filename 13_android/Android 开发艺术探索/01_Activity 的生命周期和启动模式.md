# Activity 的生命周期和启动模式

## 生命周期

### 正常生命周期

- onCreate
- onStart
- onResume
- onPause
- onStop
- onRestart
- onDestroy

 ![img](./01_Activity%20%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%92%8C%E5%90%AF%E5%8A%A8%E6%A8%A1%E5%BC%8F.assets/activity_lifecycle.png)

### 异常生命周期

#### 配置改变

系统配置发生改变后，Activity会被销毁重建，生命周期如下：

onPause -> onStop -> onSaveInstanceState -> onDestroy -> onCreate -> onStart -> onRestoreInstanceState -> onResume

#### 内存不足

内存不足时，系统会按照优先级从低到高杀死Activity所在进程，Activity 优先级如下：

前台 > 可见 > 后台

#### 常用配置

在 AndroidManifest.xml 中给activity指定 `configChanges` 属性，指定当配置发生改变时不销毁Activity重建

- mcc：移动国家号码，由三位数字组成，每个国家都有自己独立的MCC，可以识别手机用户所属国家

- mnc：移动网号，在一个国家或者地区中，用于区分手机用户的服务商

- locale：所在地区发生变化，一般指切换了系统语言
- touchscreen：触摸屏已经改变

- keyboard：键盘模式发生变化，比如用户使用外接键盘

- keyboardHidden：键盘的可访问性发生改变，比如用户调出了键盘

- navigation：系统导航方式发生变化

- screenLayout：屏幕布局发生改变

- fontScale：全局字体大小缩放发生改变
- uiMode：黑白模式切换
- orientation：屏幕方向发生改变，比如旋转手机屏幕
- screenSize：屏幕尺寸发生改变，搭配orientation使用
- smallestScreenSize：设备的屋里屏幕尺寸发生变化
- layoutDirection：布局方向发生变化

~~~xml
<!-- 黑白模式切换 -->
android:configChanges="uiMode"
<!-- 横竖屏切换 -->
android:configChanged="orientation|screenSize"
<!-- 为了确保可折叠设备能够及时响应屏幕方向和显示屏尺寸的变化 -->
android:configChanges="orientation|screenSize|screenLayout|smallestScreenSize"
~~~

*note：当配置发生改变时，在AndroidManifest.xml中指定了对应的configChanges值，则Activity不会被销毁重建，会回调`onConfigurationChanges`接口，*

*需要在该回调内做适配工作*

## 启动模式

### 四种启动模式

- standard：标准模式，系统默认启动模式。每次启动一个Activity都会重新创建一个新的实例，不管该实例是否已经存在。谁启动了这个模式的Activity，这个Activity就运行在启动它的那个Activity所在的栈中。如果使用ApplicationContext启动standard模式的Activity会报错，因为非Activity类型的Context没有任务栈

- singleTop：栈顶复用模式。要创建的Activity已经位于栈顶，则不会重新创建Activity，直接复用栈顶的Activity且回调 `onNewIntent` 方法
- singTask：栈内复用模式。只要Activity在栈内存在，则多次启动Activity都不会创建实例，会将该Activity置于栈顶并将之前的Activity全部出栈
- singInstance：单实例模式。具有此种模式的 Activity 只能单独地位于一个任务栈中

TaskAffinity：通过该属性设置Activity所在的任务栈的栈名，默认栈名为包名。属性值为字符串，且中间必须包含包名分隔符 `.`

allowTaskReparenting：通常与singleTask配对使用。

### 标志位

在配置文件中设置launchMode的优先级低于在代码中给Intent设置标志位

- FLAG_ACTIVITY_SINGLE_TASK：等价于 singleTask
- FLAG_ACTIVITY_SINGLE_TOP：等价于 singleTop

- FLAG_ACTIVITY_CLEAR_TOP：当具有该标志位的 Activity 启动时，在同一个任务栈中所有位于它上面的 Activity 都要被出栈。通常配合singleTask启动模式出现。如果被启动的 Activity 使用 standard 启动模式，那么它连同它上面的 Activity 都要被出栈，系统会创建新的 Activity 实例并置于栈顶
- FLAG_ACTIVITY_EXCLUDE_RECENTS：等价于 `android:excludeFromRecents="true"` 具有该标志位的 Activity 不会出现在历史 Activity 列表中

### adb 命令

~~~shell
adb shell dumpsys activity
adb shell dumpsys activity activities
adb shell dumpsys activity recents
~~~

## IntentFilter

### 过滤规则

一个 Activity 可以有多个 intent-filter，一个 Intent 只要能匹配其中任何一组 intent-filter 即可成功启动对应的 Activity

- action：Intent 中的 action 存在且必须和过滤规则中的其中一个 action 相同

- category：Intent 中如果存在 category，那么所有的 category 都必须和过滤规则中的其中一个 category 相同。如果想要隐式启动 Activity，必须在 Activity 的过滤规则中加上默认的 category

- data：由两部分组成，mimeType 和 URI

  - mimeType：媒体类型，例如：image/jpey、audio/mpeg4-generic、video/* 等
  - URI：<scheme>://<host>:<port>/[<path>|<pathPrefix>|<pathPattern>]
    - scheme：URI 的模式，比如 http、content 等，如果未指定 scheme，则 URI 其他参数全部无效
    - host：URI 的主机，如果 host 未指定，则 URI 其他参数全部无效
    - port：URI 的端口号，仅当 URI 中指定了 scheme 和 host 时 port 参数才有意义
    - path：完整的路径信息
    - pathPattern：完整的路径信息，但是可以包含通配符 “*”，
    - pathPrefix：表示路径的前缀信息

  ~~~xml
  <intent-filter>
  	<data android:mimeType="image/*" />
  </intent-filter>
  ~~~

  ~~~java
  intent.setDataAndType(Uri.parse("content://abc", "image/png"));
  ~~~

  如果要指定完整的data，必须调用 setDataAndType 方法，调用 setData 会把设置的 mimeType 清空，调用 setType 会把设置的 URI 清空

使用隐式启动 Activity 时，可以通过 PackageManager 的 resolveActivity 或 Intent 的 resolveActivity 方法，判断 Activity 是否存在。也可以使用 PackageManager 的 queryIntentActivities 接口

~~~java
Intent intent = new Intent();
intent.setAction("com.hcs.testconfigchanges.SecondActivity");
if (intent.resolveActivity(getPackageManager()) != null) {
    Log.d("haospring3", "onClick: ");
    startActivity(intent);
}

if (getPackageManager().resolveActivity(intent, PackageManager.MATCH_DEFAULT_ONLY) != null) {
    startActivity(intent);
}

if (getPackageManager().queryIntentActivities(intent, PackageManager.MATCH_DEFAULT_ONLY) != null) {
    startActivity(intent);
}
~~~

### window 命令

~~~shell
# adb 端口号 5037，查看端口号对应进程号
netstat -ano | findstr 5037
# 根据进程号查看对应进程名，根据进程名查看进程号
tasklist | findstr 13572
tasklist | findstr qemu-system-x86_64.exe
# 杀死进程
taskkill/PID 13572 /F
~~~

