# JSTL Core < c:url > 标签

< c:url > 标签将 URL 格式化成一个字符串，并将其存储到一个变量中。这个标签在必要时自动执行URL重写。var 属性指定将包含格式化的 URL 的变量。

JSTL url 标记只是另一种编写调用 response.encodeURL() 方法的方法。url 标签唯一的真正优势是提供了适当的 URL 编码，包括由子 param 标签指定的任何参数。

## 属性：

< c:url > 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>value</td><td>基 URL</td><td>是</td><td>无</td></tr>
<tr><td>context</td><td>/ 紧随其后的是本地 web 应用程序的名称</td><td>否</td><td style="width:25%;">当前应用程序</td></tr>
<tr><td>var</td><td>显示被处理的 URL 的变量名</td><td>否</td><td>页面输出</td></tr>
<tr><td>scope</td><td>显示被处理的 URL 的变量范围</td><td>否</td><td>页面</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;c:url&gt; Tag Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;a href="&lt;c:url value="/jsp/index.htm"/&gt;"&gt;TEST&lt;/a&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
<a href="../jsp_overview.md">TEST</a>
</pre>
