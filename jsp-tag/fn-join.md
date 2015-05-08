# JSTL fn:join() 函数

fn:join() 函数用指定的分隔符将所有的数组元素连接成一个字符串。

## 语法：

fn:join() 函数具有如下所示语法;

``` 
String join (java.lang.String[], java.lang.String)
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

&lt;p&gt;Final String : ${string3}&lt;/p&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

**注意：**fn:split() 函数返回了分成不同元素的数组。

这将产生如下所示结果：

<pre class="result notranslate">
Final String : This-is-first-String.
</pre>


