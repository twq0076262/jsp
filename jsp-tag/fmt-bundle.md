# JSTL Core < fmt:bundle > 标签

`<fmt:bundle>` 标签使指定的包对所有的出现在 `<fmt:bundle>` 和 `</fmt:bundle>` 标签之间的 `<fmt:message>` 标签是可用的。这可以节省你的额外的步骤为每个 `<fmt:message>` 标签指定资源包。


例如，下面的两个 `<fmt:bundle>` 块会产生相同的输出：

``` 
<fmt:bundle basename="com.tutorialspoint.Example">
    <fmt:message key="count.one"/>
</fmt:bundle>
<fmt:bundle basename="com.tutorialspoint.Example" prefix="count.">
    <fmt:message key="title"/>
</fmt:bundle>
```

## 属性：

`<fmt:bundle>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>basename</td><td>指定了要被加载的资源包的基名。</td><td>是</td><td>无</td></tr>
<tr><td>prefix</td><td>在 &lt;fmt:message&gt; 子标签中预先考虑的每个键值名</td><td>否</td><td>无</td></tr>
</table>

## 实例：

资源包包含特定于本地语言环境的对象。资源包包含键/值对。当你的程序需要一个特定于本地语言环境的资源时，你要把所有的键与所有的语言环境保持一致，但你可以有特定于语言环境的转换值。资源包中帮助提供特定于语言环境的内容。

一个 Java 资源包文件包含一系列 key-to-string 映射。我们关注的方法包括创建扩展 java.util.ListResourceBundle类的编译后的 Java 类。你必须编译这些类文件并使其可用于 Web 应用程序的类路径中。

让我们定义一个默认的资源包，如下所示：

``` 
package com.tutorialspoint;
import java.util.ListResourceBundle;
public class Example_En extends ListResourceBundle {
  public Object[][] getContents() {
    return contents;
  }
  static final Object[][] contents = {
  {"count.one", "One"},
  {"count.two", "Two"},
  {"count.three", "Three"},
  };
}
``` 
编译上述类 Example.class 并确保它在你的 Web 应用程序中的类路径中时可用的。现在你可以使用下面的 JSTL 标签来显示三个数字，如下所示：

<pre class="prettyprint notranslate">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;JSTL fmt:bundle Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;fmt:bundle basename="com.tutorialspoint.Example" prefix="count."&gt;
   &lt;fmt:message key="one"/&gt;&lt;br/&gt;
   &lt;fmt:message key="two"/&gt;&lt;br/&gt;
   &lt;fmt:message key="three"/&gt;&lt;br/&gt;
&lt;/fmt:bundle&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>


这会产生如下所示的结果：

<pre class="result notranslate">
One 
Two 
Three
</pre>

在不带前缀的情况下尝试上述例子，如下所示：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;JSTL fmt:bundle Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;fmt:bundle basename="com.tutorialspoint.Example"&gt;
   &lt;fmt:message key="count.one"/&gt;&lt;br/&gt;
   &lt;fmt:message key="count.two"/&gt;&lt;br/&gt;
   &lt;fmt:message key="count.three"/&gt;&lt;br/&gt;
&lt;/fmt:bundle&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这会产生如下所示的结果：

<pre class="result notranslate">
One 
Two 
Three
</pre>

查看 [**<fmt:setLocale>**](http://www.tutorialspoint.com/jsp/jstl_format_setlocale_tag.htm) 和 [**<fmt:setBundle>**](http://www.tutorialspoint.com/jsp/jstl_format_setbundle_tag.htm) 标签来理解完整内容。