# JSTL fn:endsWith() 函数

fn:endsWith() 函数决定了一个输入字符串是否由一个指定的后缀结束。

## 语法：

fn:endsWith() 函数具有如下所示语法：

``` 
boolean endsWith(java.lang.String, java.lang.String)
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

&lt;c:set var="theString" value="I am a test String 123"/&gt;

&lt;c:if test="${fn:endsWith(theString, '123')}"&gt;
   &lt;p&gt;String ends with 123&lt;p&gt;
&lt;/c:if&gt;

&lt;c:if test="${fn:endsWith(theString, 'TEST')}"&gt;
   &lt;p&gt;String ends with TEST&lt;p&gt;
&lt;/c:if&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将生成如下所示结果：

<pre class="result notranslate">
String ends with 123
</pre>

