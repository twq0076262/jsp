# JSTL fn:replace() 函数

fn:replace() 函数用一个字符串替换了另一个字符串的全部出现。

## 语法：

fn:replace() 函数具有如下所示语法：

``` 
boolean replace(java.lang.String, java.lang.String, java.lang.String)
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
&lt;c:set var="string2" value="${fn:replace(string1, 
                                'first', 'second')}" /&gt;

&lt;p&gt;Final String : ${string2}&lt;/p&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
Final String : This is second String.
</pre>

