# JSTL XML < x:out > 标签

`<x:out>` 标签显示 XPath 表达式的结果，它的作用和 JSP 语法中的 `<%= %>` 类似。

## 属性：

`<x:out>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>select</td><td>作为字符串要计算的 XPath 表达式，通常使用 XPath 变量</td><td>是</td><td>无</td></tr>
<tr><td>escapeXml</td><td>如果标签会转义特殊的 XML 字符，则为真</td><td>否</td><td>true</td></tr>
</table>

## 实例:
 
举个例子，会覆盖 (a) <x:out> (b)<x:parse> 标签。

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %&gt;
&lt;%@ taglib prefix="x" uri="http://java.sun.com/jsp/jstl/xml" %&gt;

&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;JSTL x:out Tags&lt;/title&gt;
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
&lt;b&gt;The title of the first book is&lt;/b&gt;: 
&lt;x:out select="$output/books/book[1]/name" /&gt;
&lt;br&gt;
&lt;b&gt;The price of the second book&lt;/b&gt;: 
&lt;x:out select="$output/books/book[2]/price" /&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
<h3>Books Info:</h3>
<b>The title of the first book is</b>: Padam History
<br/>
<b>The price of the second book</b>: 2000
</pre>

