# JSTL XML < x:set > 标签

`<x:set>` 标签为 XPath 表达式的值设置变量。

如果 XPath 表达式的结果是一个布尔值，<x:set> 标签就设置 java.lang.Boolean 对象；若结果是一个字符串，就设置 java.lang.String 对象；若结果是一个数值，就设置 java.lang.Number 对象。

## 属性：

`<x:set>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>var</td><td>设置 XPath 表达式值的变量</td><td>是</td><td>Body</td></tr>
<tr><td>select</td><td>要计算的 XPath 表达式</td><td>否</td><td>无</td></tr>
<tr><td>scope</td><td>在 var 属性中指定的变量范围</td><td>否</td><td>页面</td></tr>
</table>

## 实例：
 
下述例子向你展示了如何使用 `<x:set>` 标签：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %&gt;
&lt;%@ taglib prefix="x" uri="http://java.sun.com/jsp/jstl/xml" %&gt;

&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;JSTL Tags&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;h3&gt;Books Info:&lt;/h3&gt;

&lt;c:set var="xmltext"&gt;
  &lt;books&gt;
    &lt;book&gt;
      &lt;name&gt;Padam History&lt;/name&gt;
      &lt;author&gt;ZARA&lt;/author&gt;
      &lt;price&gt;100&lt;/price&gt;
    &lt;/book&gt;
    &lt;book&gt;
      &lt;name&gt;Great Mistry&lt;/name&gt;
      &lt;author&gt;NUHA&lt;/author&gt;
      &lt;price&gt;2000&lt;/price&gt;
    &lt;/book&gt;
  &lt;/books&gt;
&lt;/c:set&gt;

&lt;x:parse xml="${xmltext}" var="output"/&gt;
&lt;x:set var="fragment" select="$output//book"/&gt;
&lt;b&gt;The price of the second book&lt;/b&gt;: 
&lt;c:out value="${fragment}" /&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

现在尝试访问 JSP，会产生如下所示结果：


<pre class="result notranslate">
<h3>Books Info:</h3>
<b>The price of the second book</b>:[[book: null], [book: null]]
</pre>

