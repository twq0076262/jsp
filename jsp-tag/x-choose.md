# JSTL XML < x:choose >, < x:when >, < x:otherwise > 标签

`<x:choose>` 标签的工作方式类似于 Java 的 **switch** 语句，允许你在许多选项中进行选择。**switch** 语句有 **case** 语句，`<x:choose>` 标签有 `<x:when>` 标签。switch 语句有**缺省**子句来指定默认操作，同样的，`<x:choose>` 标签也有 `<x:otherwise>` 标签作为缺省子句。

## 属性：

- `<x:choose>` 标签没有任何属性。

- `<x:when>` 标签有一个属性，如下所示。

- `<x:otherwise>` 标签没有任何属性。

`<x:when>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>select</td><td>要计算的条件</td><td>是</td><td>无</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %&gt;
&lt;%@ taglib prefix="x" uri="http://java.sun.com/jsp/jstl/xml" %&gt;

&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;JSTL x:choose Tags&lt;/title&gt;
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
&lt;x:choose&gt;
   &lt;x:when select="$output//book/author = 'ZARA'"&gt;
      Book is written by ZARA
   &lt;/x:when&gt;
   &lt;x:when select="$output//book/author = 'NUHA'"&gt;
      Book is written by NUHA
   &lt;/x:when&gt;
   &lt;x:otherwise&gt;
      Unknown author.
   &lt;/x:otherwise&gt;
&lt;/x:choose&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
<h3>Books Info:</h3>
Book is written by ZARA
</pre>




