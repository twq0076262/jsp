# JSTL fn:escapeXml() 函数

fn:escapeXml() 函数转义了可以解释为 XML 标记的字符。

## 语法：

fn:escapeXml() 函数具有如下所示语法：

``` 
java.lang.String escapeXml(java.lang.String)
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
&lt;c:set var="string2" value="This &lt;abc&gt;is second String.&lt;/abc&gt;"/&gt;

&lt;p&gt;With escapeXml() Function:&lt;/p&gt;
&lt;p&gt;string (1) : ${fn:escapeXml(string1)}&lt;/p&gt;
&lt;p&gt;string (2) : ${fn:escapeXml(string2)}&lt;/p&gt;

&lt;p&gt;Without escapeXml() Function:&lt;/p&gt;
&lt;p&gt;string (1) : ${string1}&lt;/p&gt;
&lt;p&gt;string (2) : ${string2}&lt;/p&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
<p>With escapeXml() Function:</p>
<p>string (1) : This is first String.</p>
<p>string (2) : This &lt;abc&gt;is second String.&lt;/abc&gt;</p>
 
<p>Without escapeXml() Function:</p>
<p>string (1) : This is first String.</p>
<p>string (2) : This is second String.</p>
</pre>

