# Button 背景颜色无法改变解决办法

rect_bg.xml

~~~xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">

    <solid android:color="@color/white" />
    <corners android:radius="10dp" />
    <padding
        android:bottom="5dp"
        android:left="10dp"
        android:right="10dp"
        android:top="5dp" />
    <stroke
        android:width="1dp"
        android:color="@color/teal_200"
        android:dashWidth="5dp"
        android:dashGap="2dp" />

    <gradient
        android:angle="0"
        android:centerColor="@color/purple_200"
        android:endColor="@color/purple_500"
        android:startColor="@color/white" />
</shape>
~~~

activity_main.xml

~~~xml
<Button
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:background="@drawable/rect_bg"
    android:text="click me"
    android:textAllCaps="false"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@id/text_view" />
~~~

android:background="@drawable/rect_bg" 背景颜色不生效

项目默认主题为：*Theme.MaterialComponents.DayNight.DarkActionBar*，此主题无法修改 button 背景颜色

**解决方式一：**

1. 将主题改为 *Theme.MaterialComponents.DayNight.DarkActionBar.Bridge*
2. 将主题改为 *Theme.AppCompat下的任意一种主题 *e.g. : Theme.AppCompat.Light

**解决方式二：**

1. 布局中用 *android.widget.Button* 代替 *Button*

[参考链接: https://blog.csdn.net/weixin_52089884/article/details/122616834](https://blog.csdn.net/weixin_52089884/article/details/122616834)