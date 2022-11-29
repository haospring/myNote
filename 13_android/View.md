# View

## 一、自定义 View

### （一）构造方法

#### 1、构造方法

自定义 View 时，最少要重写前两个构造方法

~~~java
// 用于在 Java 代码中创建 View
public CustomView(Context context) {
    this(context, null);
}

// 用于在布局文件中创建 View， LayoutInflate 通过 inflate 加载View时，会通过反射调用该构造方法，参数 attrs 是在布局文件中
// 使用的属性的集合
public CustomView(Context context, AttributeSet attrs) {
    this(context, attrs, 0); 
}

public CustomView(Context context, AttributeSet attrs, int defStyleAttr) {
    this(context, attrs, defStyleAttr, 0);
}

public CustomView(Context context, AttributeSet attrs, int defStyleAttr, int defStyleRes) {
    super(context, attrs, defStyleAttr, defStyleRes);
	TypedArray ta = context.obtainStyledAttributes(attrs, R.styleable.CustomView, defStyleAttr, defStyleRes);
}
~~~

#### 2、属性使用方式

1. 在 xml 中直接定义

~~~xml
<TextView
    android:id="@+id/text_view"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/app_name"/>
~~~

2. 在 xml 中通过 style 属性引用

~~~xml
<style name="MyButtonStyle">
    <item name="textAllCaps">false</item>
</style>
<Button
    android:id="@+id/btn_test"
    style="@style/MyButtonStyle"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Test"
    app:layout_constraintBottom_toTopOf="@id/text_view"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent" />
~~~

ps：属性中`android:`一般是系统属性，定义在sdk中，`app:`一般是自定义或者控件库属性，定义在`values/attrs`中

3. 在 theme 中直接定义

~~~xml
<style name="Theme.Test" parent="Theme.AppCompat.DayNight.NoActionBar">
    <item name="android:textColor">@color/black</item>
    <item name="android:textSize">40sp</item>
</style>
<application
    android:theme="@style/Theme.Test">
</application>
~~~

主题会应用到所有的 View，作为默认的值，即使 View 没有明确定义某个属性，也会给 View 添加属性的值。

4. defStyleAttr，第三和第四个构造方法的参数

~~~xml
<style name="Theme.Test" parent="Theme.AppCompat.DayNight.NoActionBar">
    <item name="android:textViewStyle">@style/MyTextViewStyle</item>
</style>
<style name="MyTextViewStyle">
    <item name="android:textSize">20sp</item>
    <item name="android:textColor">@color/purple_200</item>
</style>
~~~

textViewStyle 定义在 `sdk/platforms/android-xx/data/res/values` 的 `attrs.xml` 中

之所以在主题中定义`android:textViewStyle`会应用到所有的TextView，是因为在TextView的构造方法中使用该属性作为`defStyleAttr`

~~~xml
public TextView(Context context, @Nullable AttributeSet attrs) {
    this(context, attrs, com.android.internal.R.attr.textViewStyle);
}
~~~

5. defStyleRes：第四个构造函数中的参数，直接使用系统主题样式

**生效优先级：xml 中直接使用 > xml 中通过 style 引用 > defStyleAttr > defStyleRes > theme 直接定义**

#### 3、参数解析

`obtainStyledAttributes(AttributeSet set, int[] attrs, int defStyleAttr, int defStyleRes)`

- set：从布局文件中直接为这个`View`添加的属性的集合

- attrs：需要获取的属性集合
- defStyleAttr：定义可以直接在 Theme 中使用的的属性（e.g. TextView，textViewStyle）
- defStyleRes：直接从资源文件中定义的某个样式中读取

### （二）自定义属性





