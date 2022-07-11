### ToolBar

1. 在布局文件中加入ToolBar的布局

~~~xml
<androidx.appcompat.widget.Toolbar
        android:id="@+id/my_toolbar"
        android:layout_width="match_parent"
        android:layout_height="?attr/actionBarSize"
        android:background="?attr/colorPrimary"
        android:elevation="4dp"
        android:theme="@style/ThemeOverlay.AppCompat.ActionBar"
        app:popupTheme="@style/ThemeOverlay.AppCompat.Light"
        tools:ignore="MissingConstraints" />
~~~

2. 在 AndroidManifest.xml 文件的 application 标签中使用不带 Actionbar 的主题样式

~~~xml
android:theme="@style/Theme.AppCompat.Light.NoActionBar"
~~~

3. 在oncreate()中替换掉Actionbar

~~~java
Toolbar toolbar = findViewById(R.id.my_toolbar);
setSupportActionBar(toolbar);
~~~

4. 获取Actionbar，可以使用Actionbar的方法

~~~java
ActionBar actionBar = getSupportActionBar();
actionBar.hide();
actionBar.show();
~~~

### Menu

1. 在res目录下新建menu目录，创建menu资源

~~~xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:id="@+id/menu_favorite"
        android:icon="@drawable/heart"
        android:title="love"
        app:showAsAction="ifRoom" />

    <item
        android:id="@+id/menu_add"
        android:icon="@drawable/add"
        android:title="add"
        app:showAsAction="never" />

</menu>
~~~

2. menu属性

~~~xml
android:id="@+id/menu_favorite"
<!-- 当item在应用栏时，显示图标，当item在溢出栏时，显示文字 -->
android:icon="@drawable/heart"
android:title="love"
<!-- 
默认情况下，系统会将所有菜单项放入操作溢出菜单中
ifRoom：如果应用栏有空间，则显示在应用栏，否在显示在溢出菜单
never：不显示在应用栏
always：只显示在溢出菜单，可能导致界面重叠
collapseActionView：如果微件位于应用栏中，则显示图标。如果微件位于溢出菜单中，则显示为菜单项。当用户与操作视图互动时，它应该展开以填满应用栏
withText：还会随操作项添加标题文本，可以将此值与某个其他值一起作为标记集添加，用竖线 | 分隔
-->
app:showAsAction="ifRoom"
~~~

3. 应用栏左侧返回图标

~~~java
# 在onCreate()中
getSupportActionBar().setDisplayHomeAsUpEnabled(true);
~~~

~~~xml
<!-- 在AndroidManifest.xml中给activity添加parentActivityName属性 -->
android:parentActivityName="com.mitac.android.myapplicationcode.MainActivity"
<!-- Parent activity meta-data to support 4.0 and lower -->
<meta-data
           android:name="android.support.PARENT_ACTIVITY"
           android:value=".MainActivity" />
~~~

~~~java
# 在Activity中重写onOptionsItemSelected方法
switch (item.getItemId()) {
    case android.R.id.home:
        onBackPressed();
        break;
~~~

4. 添加搜索框

~~~xml
<!-- 给menu添加新的item -->
<item
      android:id="@+id/menu_search"
      android:icon="@drawable/search"
      android:title="search"
      app:showAsAction="ifRoom|collapseActionView"
      app:actionViewClass="androidx.appcompat.widget.SearchView" />
~~~

~~~java
# 在onCreateOptionsMenu中获取到SearchView空间
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.test_menu, menu);

    MenuItem searchItem = menu.findItem(R.id.menu_search);
    SearchView = (SearchView) searchItem.getActionView();

    # 添加折叠/展开监听
    searchItem.setOnActionExpandListener(new MenuItem.OnActionExpandListener() {
        @Override
        public boolean onMenuItemActionExpand(MenuItem item) {
            Log.i(TAG, "onMenuItemActionExpand: ");
            return true;
        }

        @Override
        public boolean onMenuItemActionCollapse(MenuItem item) {
            Log.i(TAG, "onMenuItemActionCollapse: ");
            return true;
        }
    });
    return true;
}
~~~



