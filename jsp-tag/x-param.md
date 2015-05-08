# JSTL XML < x:param > 标签

`<x:param>` 标签和转换标签一起使用来设置 XSLT 样式表中的参数。

## 属性：

`<x:param>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>name</td><td>要设置的 XSLT 参数名</td><td>是</td><td>Body</td></tr>
<tr><td>value</td><td>要设置的 XSLT 参数值</td><td>否</td><td>无</td></tr>
</table>

## 实例：

考虑下述 XSLT 样式表 style.xsl。注意 `<xsl:param...>` 标签和变量 {$bgColor} 的使用：

<pre class="prettyprint notranslate">
&lt;?xml version="1.0"?&gt;
&lt;xsl:stylesheet xmlns:xsl=
"http://www.w3.org/1999/XSL/Transform" version="1.0"&gt;

&lt;xsl:output method="html" indent="yes"/&gt;
&lt;xsl:param name="bgColor"/&gt;

&lt;xsl:template match="/"&gt;
  &lt;html&gt;
  &lt;body&gt;
   &lt;xsl:apply-templates/&gt;
  &lt;/body&gt;
  &lt;/html&gt;
&lt;/xsl:template&gt;

&lt;xsl:template match="books"&gt;
  &lt;table border="1" width="50%" bgColor="{$bgColor}"&gt;
    &lt;xsl:for-each select="book"&gt;
      &lt;tr&gt;
        &lt;td&gt;
          &lt;i&gt;&lt;xsl:value-of select="name"/&gt;&lt;/i&gt;
        &lt;/td&gt;
        &lt;td&gt;
          &lt;xsl:value-of select="author"/&gt;
        &lt;/td&gt;
        &lt;td&gt;
          &lt;xsl:value-of select="price"/&gt;
        &lt;/td&gt;
      &lt;/tr&gt;
    &lt;/xsl:for-each&gt;
  &lt;/table&gt;
&lt;/xsl:template&gt;
&lt;/xsl:stylesheet&gt;
</pre>

现在考虑如下所示的 JSP 文件，其中我们在 `<x:transform>` 标签内用 `<x:param>` 标签定义了 bgColor 的值：

<pre class="prettyprint notranslate">
&lt;%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %&gt;
&lt;%@ taglib prefix="x" uri="http://java.sun.com/jsp/jstl/xml" %&gt;

&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;JSTL x:transform Tags&lt;/title&gt;
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

&lt;c:import url="http://localhost:8080/style.xsl" var="xslt"/&gt;
&lt;x:transform xml="${xmltext}" xslt="${xslt}"&gt;
   &lt;x:param name="bgColor" value="grey"/&gt;
&lt;/x:transform&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
<h3>Books Info:</h3>
<table width="100%" border="1" bgColor="grey">
<tr>
<td><i>Padam History</i></td><td>ZARA</td><td>100</td>
</tr>
<tr>
<td><i>Great Mistry</i></td><td>NUHA</td><td>2000</td>
</tr>
</table>
</pre>

