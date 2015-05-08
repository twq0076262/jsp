# JSTL fn:substringAfter() 函数

fn:substringAfter() 函数在指定的子字符串后返回字符串的一部分。

## 语法：

fn:substringAfter() 函数具有如下所示语法：

``` 
java.lang.String substringAfter(java.lang.String, java.lang.String)
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
&lt;c:set var="string2" value="${fn:substringAfter(string1, 'is')}" /&gt;

&lt;p&gt;Final sub string : ${string2}&lt;/p&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
Final sub string : is first String.
</pre>
