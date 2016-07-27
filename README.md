# Style

Lesson96 Style and Theme
1.Style:样式，是给View或Window指定外观和格式的属性集合，样式能指定如高/边距/字体颜色/字体尺寸/背景颜色等属性，样式被定义在一个与         布局XML文件分开的XML资源文件中，允许与内容分开设计。
  --使用样式属性：
  <TextView
    //--样式格式写法
    style="@style/CodeFont"     //引用样式的名字，如引用下面的实例中的CodeFont样式 
    android:tex="@string/hello"/>
  --如何定义样式：创建一个样式文件保存为XML格式，保存在res/values/目录下，且XML文件中root根节点必须是<resources>.对于要创建的每个                 样式，都要在这个XML文件中添加一个<style>元素，并用name属性唯一标识这个样式（这个属性是必须的），然后给样式的每                 个属性添加一个<item>元素，这个元素的name属性用于声明样式属性名即要定义什么属性，属性值放在一组<item>之间，给
                  <item>元素的值可以是一个字符串/十六进制的颜色/另一个资源类型的引用/或者依赖样式属性的其他值。如下实例：
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
    --<resource>元素的每个子元素在编译时都要被转换成一个应用程序资源对象，通过<style>元素的name属性值来引用，记住：把XML中定义   的一个样式用作一个Activity或应用程序的主题与给一个View对象定义样式完全相同，如上面定义的样式能够用于一个View对象，或者用   作一个Activity或者应用程序的主题.实际上运用到View上就是样式，运用到Activity就是主题.
