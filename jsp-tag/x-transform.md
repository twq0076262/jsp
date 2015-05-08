# JSTL XML < x:transform > 标签

`<x:transform>` 标签用于 XML 文档中的 XML 转换。

## 属性：

`<x:transform>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>doc</td><td>XSLT 转换的源 XML 文档</td><td>否</td><td>Body</td></tr>
<tr><td>docSystemId</td><td>初始 XML 文档的 URI</td><td>否</td><td>无</td></tr>
<tr><td>xslt</td><td>XSLT 样式表提供转换指导</td><td>是</td><td>无</td></tr>
<tr><td>xsltSystemId</td><td>初始 XSLT 文档的 URI</td><td>否</td><td>无</td></tr>
<tr><td>result</td><td>接收转换结果的结果对象</td><td>否</td><td>页面输出</td></tr>
<tr><td>var</td><td>设置为转换的 XML 文档的变量</td><td>否</td><td>页面输出</td></tr>
<tr><td>scope</td><td>显示转换结果的变量范围</td><td>否</td><td>无</td></tr>
</table>

## 实例：

考虑如下所示的 XSLT 样式表 style.xsl：

<pre class="prettyprint notranslate">
&lt;?xml version="1.0"?&gt;
&lt;xsl:stylesheet xmlns:xsl=
"http://www.w3.org/1999/XSL/Transform" version="1.0"&gt;

&lt;xsl:output method="html" indent="yes"/&gt;

&lt;xsl:template match="/"&gt;
  &lt;html&gt;
  &lt;body&gt;
   &lt;xsl:apply-templates/&gt;
  &lt;/body&gt;
  &lt;/html&gt;
&lt;/xsl:template&gt;

&lt;xsl:template match="books"&gt;
  &lt;table border="1" width="100%"&gt;
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

现在考虑如下所示的 JSP 文件：

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
&lt;x:transform xml="${xmltext}" xslt="${xslt}"/&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示的结果：

<pre class="result notranslate">
<h3>Books Info:</h3>
<table width="100%" border="1">
<tr>
<td><i>Padam History</i></td><td>ZARA</td><td>100</td>
</tr>
<tr>
<td><i>Great Mistry</i></td><td>NUHA</td><td>2000</td>
</tr>
</table>
</pre>
