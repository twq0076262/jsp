# JSTL XML < x:parse > 标签

< x:parse > 标签用于解析通过一个属性或在标签本体中指定的 MXL 数据。

## 属性：

< x:parse > 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>var</td><td>包含解析的 XML 数据的变量</td><td>否</td><td>无</td></tr>
<tr><td>xml</td><td>要解析的文档文本 (String 或 Reader)</td><td>否</td><td>Body</td></tr>
<tr><td>systemId</td><td>解析文档的系统标识符 URI</td><td>否</td><td>无</td></tr>
<tr><td>filter</td><td>应用于源文档的过滤器</td><td>否</td><td>无</td></tr>
<tr><td>doc</td><td>要被解析的 XML 文档</td><td>否</td><td>页面</td></tr>
<tr><td>scope</td><td>在 var 属性中指定的变量范围</td><td>否</td><td>页面</td></tr>
<tr><td>varDom</td><td>包含解析的 XML 数据的变量</td><td>否</td><td>页面</td></tr>
<tr><td>scopeDom</td><td>在 varDom 属性中指定的变量范围</td><td>否</td><td>页面</td></tr>
</table>

## 实例：

下述的例子中描述了解析是怎样用来读取和解析外部的 XML 文件的：

我们已经理解了怎样从给定的文档中的主体解析 XML。现在将下述内容放到 books.xml 文件中：

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

现在尝试下述的 main.jsp，并保存在相同的目录中：

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

现在用 http://localhost:8080/main.jsp 尝试访问上述 JSP，这会产生如下所示结果：

<pre class="result notranslate">
<h3>Books Info:</h3>
<p><b>The title of the first book is</b>:Padam History</p>
<p><b>The price of the second book</b>: 2000</p>
</pre>




