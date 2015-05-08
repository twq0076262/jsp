# JSTL Core < fmt:setLocale > 标签

< fmt:setLocale > 标签用于在语言环境配置变量中存储给定的语言环境。

## 属性：

< fmt:setLocale > 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th width="15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>value</td><td>指定了一个两部分代码，代表 ISO-639 语言代码和 ISO-3166 国家代码。</td><td>是</td><td>en_US</td></tr>
<tr><td>variant</td><td>浏览器特定的变量</td><td>否</td><td>无</td></tr>
<tr><td>scope</td><td>语言环境配置变量的范围</td><td>否</td><td>页面</td></tr>
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
现在让我们再定义一个资源包，使用西班牙语：

``` 
package com.tutorialspoint;

import java.util.ListResourceBundle;

public class Example_es_ES extends ListResourceBundle {
  public Object[][] getContents() {
    return contents;
  }
  static final Object[][] contents = {
  {"count.one", "Uno"},
  {"count.two", "Dos"},
  {"count.three", "Tres"},
  };
}
```

编译上述类 Example.class 和 Example_es_ES.class，确保它们在你的 Web 应用程序中的类路径中是可用的。现在你可以使用下面的 JSTL 标签来显示三个数字，如下所示：

<pre class="prettyprint notranslate">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;JSTL fmt:setLocale Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;fmt:bundle basename="com.tutorialspoint.Example"&gt;
   &lt;fmt:message key="count.one"/&gt;&lt;br/&gt;
   &lt;fmt:message key="count.two"/&gt;&lt;br/&gt;
   &lt;fmt:message key="count.three"/&gt;&lt;br/&gt;
&lt;/fmt:bundle&gt;

&lt;!-- Change the Locale --&gt;
&lt;fmt:setLocale value="es_ES"/&gt;
&lt;fmt:bundle basename="com.tutorialspoint.Example"&gt;
   &lt;fmt:message key="count.one"/&gt;&lt;br/&gt;
   &lt;fmt:message key="count.two"/&gt;&lt;br/&gt;
   &lt;fmt:message key="count.three"/&gt;&lt;br/&gt;
&lt;/fmt:bundle&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
One 
Two 
Three
Uno
Dos
Tres
</pre>

查看 [**<fmt:bundle>**](http://www.tutorialspoint.com/jsp/jstl_format_bundle_tag.htm) 和 [**<fmt:setBundle>**](http://www.tutorialspoint.com/jsp/jstl_format_setbundle_tag.htm) 标签来理解完整内容。

