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

#### 解决方式

在 AndroidManifest.xml 中给activity指定 `configChanges` 属性，指定当配置发生改变时不销毁Activity重建

**常用配置**

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

- standard：标准模式，系统默认启动模式。每次启动一个Activity都会重新创建一个新的实例，不管该实例是否已经存在。谁启动了这个模式的Activity，这个Activity就运行在启动它的那个Activity所在的栈中