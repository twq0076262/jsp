# JSTL XML < x:if > 标签

`<x:if>` 标签计算了一个测试 XPath 表达式，如果测试条件为真，则处理它的主体，如果测试条件为假，主体就被忽略。

## 属性：

`<x:if>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>select</td><td>要计算的 XPath 表达式</td><td>是</td><td>无</td></tr>
<tr><td>var</td><td>存储条件结果的变量名</td><td>否</td><td>无</td></tr>
<tr><td>scope</td><td>在 var 属性中指定的变量范围</td><td>无</td><td>页面</td></tr>
</table>

## 实例：

下述例子向你展示了如何使用 `<x:if>` 标签：

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

&lt;x:if select="$output//book"&gt;
   Document has at least one &lt;book&gt; element.
&lt;/x:if&gt;
&lt;br /&gt;
&lt;x:if select="$output/books[1]/book/price &gt; 100"&gt;
   Book prices are very high
&lt;/x:if&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

现在尝试访问 JSP，将会产生如下所示结果：

<pre class="result notranslate">
<h3>Books Info:</h3>
Document has at least one &lt;book&gt; element.
<br />
Book prices are very high
</pre>

