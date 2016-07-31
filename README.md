# Style

Lesson96-97 Style and Theme

1.Style:样式，是给View或Window指定外观和格式的属性集合，样式能指定如高/边距/字体颜色/字体尺寸/背景颜色等属性，样式被定义在一个与布局XML文件分开的XML资源文件   中，允许与内容分开设计。
  --使用样式属性：
  <TextView
    //--样式格式写法
    style="@style/CodeFont"     //引用样式的名字，如引用下面的实例中的CodeFont样式 
    android:tex="@string/hello"/>
  --如何定义样式：创建一个样式文件保存为XML格式，保存在res/values/目录下，且XML文件中root根节点必须是<resources>.对于要创建的每个样式，都要在这个XML文件中添加一个<style>元素，并用name属性唯一标识这个样式（这个属性是必须的），然后给样式的每个属性添加一个<item>元素，这个元素的name属性用于声明样式属性名即要定义什么属性，属性值放在一组<item>之间，给<item>元素的值可以是一个字符串/十六进制的颜色/另一个资源类型的引用/或者依赖样式属性的其他值。如下实例：
    <?xml version="1.0" encoding="utf-8"?>
    //--通过样式名称来调用该样式，即用style="@style/CodeFont"来引用该样式
    <resources>
        //--parent是一个继承，指定了另一个样式的资源ID，继承一个其他样式
        <style name="CodeFont" parent="@android:style/TextAppearance.Medium">  
            <item name="android:layout_width">fill_parent</item>
            <item name="android:layout_height">wrap_content</item>
            <item name="android:textColor">#00FF00</item>
            <item name="android:typeface">monospace</item>
        </style>
    </resources>
    --<resource>元素的每个子元素在编译时都要被转换成一个应用程序资源对象，通过<style>元素的name属性值来引用，记住：把XML中定义的一个样式用作一个Activity或应用程序的主题与给一个View对象定义样式完全相同，如上面定义的样式能够用于一个View对象，或者用作一个Activity或者应用程序的主题.实际上运用到View上就是样式，运用到Activity就是主题.

2.样式继承性：<style>元素中的parent属性可以继承一个即存在的样式属性，然后只定义需要改变和添加的属性，你能够继承自己定义的样式，也可以继承平台内置的样式。如 
             上面的实例中parent="@android:style/TextAppearance.Medium"就是继承平台内置的样式.
  --如果要继承自己定义的样式，就不必使用parent属性，但是要把想要继承的样式名做新样式名的前缀(用点分开)。如创建一个新的继承上面定义的CodeFont样式的样式，但
    要使用红色的文件，可以设计以下新样式：
    <style name="CodeFont.Red">   
            <item name="android:textColor">#FF0000</item> 
    </style>
    可以有多层继承，如继承CodeFont和CodeFont.Red的同时，添加一个属性：
    <style name="CodeFont.Red.Big">
        <item name="android:textSize">60sp</item>
    </style>
    --注意：这种通过把名字链接在一起的继承性只对自己定义的样式有效，不能用这种方法来继承android内置的样式，要引用内置的样式，         必须使用parent属性.

3.样式实例：
  在res->values->新建一个样式style96.xml样式:
  <?xml version="1.0" encoding="utf-8"?>
  <resources>
    <style name="CodeFont" parent="@android:style/TextAppearance.Medium"> //继承平台内部的样式要用parent
        <item name="android:layout_width">fill_parent</item>
        <item name="android:layout_height">wrap_content</item>
        <item name="android:textColor">#00FF00</item>
        <item name="android:textSize">30sp</item>
        <item name="android:typeface">monospace</item>
    </style>
    <style name="CodeFont.Red">  //继承自己定义的样式，不需要parent，但要用继承的样式名做新样式名的前缀+.+自己的名字
        <item name="android:textColor">#FF0000</item>
    </style>
  </resources>

  把要用到的字符串写入res->values->strings.xml:
  <resources>
    <string name="app_name">Android_96</string>
    <string name="text96">Hello World!</string>
  </resources>
  
  在布局文件res->layout->activtiy_main.xml中引用样式：
  <?xml version="1.0" encoding="utf-8"?>
  <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.mackerlee.android_96.MainActivity">

    <TextView
        style="@style/CodeFont.Red"
        android:text="@string/text96" />
  </RelativeLayout>
  
4.Themes主题：主题是应用于整个Activity或应用程序的样式，而不是一个独立的View对象，当一个样式被用作主题时，Activity或应用程序中
              的每个View对象都会使用它所支持的每个样式属性，主题是运用在清单文件里面.
  --如果View中具体运用了样式，则样式会覆盖掉主题；
  --自定义主题首先必须继承系统里生成的主题，如下实例：
  在res->values->styles96.xml里再定义一个继承系统里的主题的样式AppTheme.Red：
  <?xml version="1.0" encoding="utf-8"?>
  <resources>
      <style name="CodeFont" parent="@android:style/TextAppearance.Medium">
          <item name="android:layout_width">fill_parent</item>
          <item name="android:layout_height">wrap_content</item>
          <item name="android:textColor">#00FF00</item>
          <item name="android:textSize">30sp</item>
          <item name="android:typeface">monospace</item>
      </style>
      <style name="CodeFont.Green">
          <item name="android:textColor">#00FF00</item>
      </style>
      <style name="CodeFont.Green.Big">
          <item name="android:textSize">60sp</item>
      </style>
      <style name="AppTheme.Red">
          <item name="android:textColor">#FF0000</item>
          <item name="android:textSize">60sp</item>
      </style>
  </resources>
  将AppTheme.Red运用于主题在清单文件中：有两种方式
  <?xml version="1.0" encoding="utf-8"?>
  <manifest xmlns:android="http://schemas.android.com/apk/res/android"
      package="com.example.mackerlee.android_96">
  
      <application
          android:allowBackup="true"
          android:icon="@mipmap/ic_launcher"
          android:label="@string/app_name"
          android:supportsRtl="true"
          android:theme="@style/AppTheme">  //方式一运用主题
          <activity
              android:name=".MainActivity"
              android:theme="@style/AppTheme.Red"> //方式二运用主题，该例在这里运用自定义主题
              <intent-filter>
                  <action android:name="android.intent.action.MAIN" />
  
                  <category android:name="android.intent.category.LAUNCHER" />
              </intent-filter>
          </activity>
      </application>
  
  </manifest>
  在activity_main.xml中再定义一个TextView用于测试：
  <?xml version="1.0" encoding="utf-8"?>
  <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:paddingBottom="@dimen/activity_vertical_margin"
      android:paddingLeft="@dimen/activity_horizontal_margin"
      android:paddingRight="@dimen/activity_horizontal_margin"
      android:paddingTop="@dimen/activity_vertical_margin"
      tools:context="com.example.mackerlee.android_96.MainActivity">
  
      <TextView
          style="@style/CodeFont.Green"
          android:text="@string/text96"
          android:id="@+id/textView96" />
  
      <TextView
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:textAppearance="?android:attr/textAppearanceLarge"
          android:text="@string/text97"
          android:id="@+id/textView97"
          android:layout_below="@+id/textView96"
          android:layout_alignParentStart="true"
          android:layout_marginTop="73dp" />
  </RelativeLayout>
 
