# JSTL XML < x:forEach > 标签

`<x:forEach>` 标签用于在 XML 文档中的代码中循环。

## 属性：

`<x:forEach>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>select</td><td>要计算的 XPath 表达式</td><td>是</td><td>无</td></tr>
<tr><td>var</td><td>每次循环中存储当前项目的变量名</td><td>否</td><td>无</td></tr>
<tr><td>begin</td><td>迭代的开始指针</td><td>否</td><td>无</td></tr>
<tr><td>end</td><td>迭代的结束指针</td><td>否</td><td>无</td></tr>
<tr><td>step</td><td>遍历集合时指针增量的大小</td><td>否</td><td>无</td></tr>
<tr><td>varStatus</td><td>存储的迭代状态的变量名</td><td>否</td><td>无</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %&gt;
&lt;%@ taglib prefix="x" uri="http://java.sun.com/jsp/jstl/xml" %&gt;

&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;JSTL x:if Tags&lt;/title&gt;
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
&lt;ul class="list"&gt;
&lt;x:forEach select="$output/books/book/name" var="item"&gt;
   &lt;li&gt;Book Name: &lt;x:out select="$item" /&gt;&lt;/li&gt;
&lt;/x:forEach&gt;
&lt;/ul&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
<h3>Books Info:</h3>
<ul class="list">
   <li><p>Book Name: Padam History</p></li>
   <li><p>Book Name: Great Mistry</p></li>
</ul>
</pre>
