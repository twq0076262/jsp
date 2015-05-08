# JSTL fn:indexOf() 函数

fn:indexOf() 函数返回指定的子字符串的指针。

## 语法：

fn:indexOf() 函数具有如下所示语法：

``` 
int indexOf(java.lang.String, java.lang.String)
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

&lt;p&gt;Index (1) : ${fn:indexOf(string1, "first")}&lt;/p&gt;
&lt;p&gt;Index (2) : ${fn:indexOf(string2, "second")}&lt;/p&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
Index (1) : 8
Index (2) : 13
</pre>
