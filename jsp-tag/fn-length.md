# JSTL fn:length() 函数

fn:length() 函数返回字符串的长度或集合中项目的数量。

## 语法：

fn:length() 函数具有如下所示语法：

``` 
int length(java.lang.Object)
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
&lt;c:set var="string2" value="This is second String." /&gt;

&lt;p&gt;Length of String (1) : ${fn:length(string1)}&lt;/p&gt;
&lt;p&gt;Length of String (2) : ${fn:length(string2)}&lt;/p&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
Length of String (1) : 21
Length of String (2) : 22
</pre>
