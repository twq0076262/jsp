# JSTL fn:startsWith() 函数

fn:startsWith() 函数决定了一个输入字符串是否以一个指定的子字符串开始。

## 语法：

fn:startsWith() 函数具有如下所示的语法：

``` 
boolean startsWith(java.lang.String, java.lang.String)
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

&lt;c:set var="string" value="Second: This is first String."/&gt;
&lt;c:if test="${fn:startsWith(string, 'First')}"&gt;
   &lt;p&gt;String starts with First&lt;/p&gt;
&lt;/c:if&gt;
&lt;br /&gt;
&lt;c:if test="${fn:startsWith(string, 'Second')}"&gt;
   &lt;p&gt;String starts with Second&lt;/p&gt;
&lt;/c:if&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
String starts with Second
</pre>
