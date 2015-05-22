# JSP - XML 数据 

当你通过 HTTP 发送 XML 数据时，使用 JSP 处理传入和传出的XML文件是有意义的，例如 RSS 文档。作为 XML 文档仅仅是一堆文字，通过 JSP 创建一个 XML 文档并不比创建一个 HTML 文档困难。 

## 从 JSP 发送 XML

你可以用 JSPs 发送 HTML 的同样的方式来发送 XML 内容。唯一的区别在于，你必须设置页面的内容类型为 text/xml。使用 < % @page % > 标签来设置内容类型，如下所示：

``` 
<%@ page contentType="text/xml" %>
```

下面是一个简单的例子将 XML 内容发送到浏览器：

``` 
<%@ page contentType="text/xml" %>
<books>
   <book>
      <name>Padam History</name>
      <author>ZARA</author>
      <price>100</price>
   </book>
</books>
```

尝试使用不同的浏览器访问上面的 XML，用来显示上面的 XML 的文档树。 

## 在 JSP 上处理 XML 
 
在使用 JSP 处理 XML 之前，你需要复制以下两个 XML 和 XPath 相关的库到你的 <Tomcat Installation Directory>\lib 中： 

- **XercesImpl.jar:**  从 [http://www.apache.org/dist/xerces/j/](http://www.apache.org/dist/xerces/j/) 下载

- **xalan.jar:**  从 [http://xml.apache.org/xalan-j/index.html](http://xml.apache.org/xalan-j/index.html) 下载

让我们把以下内容放入 books.xml 文件：

``` 
<books>
<book>
  <name>Padam History</name>
  <author>ZARA</author>
  <price>100</price>
</book>
<book>
  <name>Great Mistry</name>
  <author>NUHA</author>
  <price>2000</price>
</book>
</books>
```

现在尝试写以下 main.jsp，将其放在同一个目录下：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %&gt;
&lt;%@ taglib prefix="x" uri="http://java.sun.com/jsp/jstl/xml" %&gt;
 
&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;JSTL x:parse Tags&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;h3&gt;Books Info:&lt;/h3&gt;
&lt;c:import var="bookInfo" url="http://localhost:8080/books.xml"/&gt;
 
&lt;x:parse xml="${bookInfo}" var="output"/&gt;
&lt;b&gt;The title of the first book is&lt;/b&gt;: 
&lt;x:out select="$output/books/book[1]/name" /&gt;
&lt;br&gt;
&lt;b&gt;The price of the second book&lt;/b&gt;: 
&lt;x:out select="$output/books/book[2]/price" /&gt;
 
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在尝试使用 http://localhost:8080/main.jsp 访问上述 JSP，产生的结果如下所示：

<pre class="result notranslate">
<h3>Books Info:</h3>
<b>The title of the first book is</b>:Padam History
<br/>
<b>The price of the second book</b>: 2000
</pre>


## 格式化 XML 和 JSP 

考虑下面的 XSLT 样式表 style.xsl：

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


现在考虑下面的 JSP 文件：

<pre class="prettyprint notranslate tryit">
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

产生的结果如下所示：

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


关于用 JSTL 处理 XML 更多的细节，你可以查询 [**JSP Standard Tag Library**](standard_tag_library.htm)。
