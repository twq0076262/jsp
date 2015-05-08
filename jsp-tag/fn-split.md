# JSTL fn:split() 函数

fn:split() 函数将一个字符串划分为基于分隔符字符串的一组子字符串。

## 语法：

fn:split() 函数具有如下所示语法：

``` 
java.lang.String[] split(java.lang.String, java.lang.String)
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
&lt;c:set var="string2" value="${fn:split(string1, ' ')}" /&gt;
&lt;c:set var="string3" value="${fn:join(string2, '-')}" /&gt;

&lt;p&gt;String (3) : ${string3}&lt;/p&gt;

&lt;c:set var="string4" value="${fn:split(string3, '-')}" /&gt;
&lt;c:set var="string5" value="${fn:join(string4, ' ')}" /&gt;

&lt;p&gt;String (5) : ${string5}&lt;/p&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
String (3) : This-is-first-String.
String (5) : This is first String.
</pre>
