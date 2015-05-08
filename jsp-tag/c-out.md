# JSTL Core < c:out > 标签

< c:out > 标签显示表达式的结果，与 <%= %> 的工作方式类似，但有一点不同是 <c:out> 标签让你使用更简单的 "." 符号来访问属性。例如，访问 customer.address.street 只需要使用 <c:out value="customer.address.street"/> 就可以了。

< c:out > 标签可以自动转义 XML 标记,所以它们并不像实际标签一样被评估。

## 属性：

<c:out> 标签有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>value</td><td>输出的信息</td><td>是</td><td>无</td></tr>
<tr><td>default</td><td>输出的反馈信息</td><td>否</td><td>body</td></tr>
<tr><td>escapeXml</td><td>如果该标签被转义为特殊的 XML 字符，则为真</td><td>否</td><td>真</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;c:out&gt; Tag Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;c:out value="${'&lt;tag&gt; , &amp;'}"/&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
&lt;tag&gt; , &amp;
</pre>
