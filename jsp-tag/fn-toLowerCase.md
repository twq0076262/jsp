# JSTL fn:toLowerCase() 函数

fn:toLowerCase() 函数讲一个字符串的所有字符转换为小写字符。

## 语法：

fn:toLowerCase() 函数具有如下所示语法：

``` 
java.lang.String toLowerCase(java.lang.String)
``` 

## 实例：

下述例子解释了该函数的功能：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Using JSTL Functions&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;c:set var="string1" value="This is first String."/&gt;
&lt;c:set var="string2" value="${fn:toLowerCase(string1)}" /&gt;

&lt;p&gt;Final string : ${string2}&lt;/p&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
Final string : this is first string.
</pre>
