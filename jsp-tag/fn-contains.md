# JSTL fn:contains() 函数

fn:contains() 函数决定了一个输入字符串是否包含一个指定的子字符串。

## 语法：

fn:contains() 函数有如下所示语法：

``` 
boolean contains(java.lang.String, java.lang.String)
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

&lt;c:set var="theString" value="I am a test String"/&gt;

&lt;c:if test="${fn:contains(theString, 'test')}"&gt;
   &lt;p&gt;Found test string&lt;p&gt;
&lt;/c:if&gt;

&lt;c:if test="${fn:contains(theString, 'TEST')}"&gt;
   &lt;p&gt;Found TEST string&lt;p&gt;
&lt;/c:if&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
Found test string
</pre>
