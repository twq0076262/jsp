# JSTL fn:trim() 函数

fn:trim() 函数将字符串两端的空白删除。

## 语法：

fn:trim() 函数具有如下所示语法：

``` 
java.lang.String trim(java.lang.String)
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

&lt;c:set var="string1" value="This is first String         "/&gt;
&lt;p&gt;String (1) Length : ${fn:length(string1)}&lt;/p&gt;

&lt;c:set var="string2" value="${fn:trim(string1)}" /&gt;
&lt;p&gt;String (2) Length : ${fn:length(string2)}&lt;/p&gt;
&lt;p&gt;Final string : ${string2}&lt;/p&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
String (1) Length : 29
String (2) Length : 20
Final string : This is first String
</pre>


