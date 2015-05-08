# JSTL Core < fmt:requestEncoding > 标签

`<fmt:requestEncoding>` 标签用于指定编码类型，该编码类型用于将数据传回到 Web 应用程序的表单中。

## 属性：

`<fmt:requestEncoding>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>key</td><td>当解码请求参数时，你想要应用的字符编码的名称</td><td>是</td><td>无</td></tr>
</table>

当你想要为从表单发送的解码数据指定字符编码时，你就会用到 < fmt:requestEncoding > 标签。该标签必须和与 ISO-8859-1 不同的字符编码一起使用。由于大多数浏览器在它们的请求中不包括内容类型的头信息，所以这个标签是必需的。

`<fmt:requestEncoding>` 标签的目的是指定请求的内容类型。你必须指定内容类型，即使页面编码生成的响应式通过页面指令的内容类型属性指定的。这是因为响应的实际语言环境（以及字符编码）可能与页面指令中指定的值不同。

如果页面包含一个 I18N-capable 格式化操作，通过调用 ServletResponse.setLocale() 设置了响应的语言环境（以及字符编码），任何在页面指令中指定的编码都将被覆盖。

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;JSTL fmt:message Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;fmt:requestEncoding value="UTF-8" /&gt;
&lt;fmt:setLocale value="es_ES"/&gt;
&lt;fmt:setBundle basename="com.tutorialspoint.Example" var="lang"/&gt;

&lt;fmt:message key="count.one" bundle="${lang}"/&gt;&lt;br/&gt;
&lt;fmt:message key="count.two" bundle="${lang}"/&gt;&lt;br/&gt;
&lt;fmt:message key="count.three" bundle="${lang}"/&gt;&lt;br/&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示的结果：

<pre class="result notranslate">
Uno
Dos
Tres
</pre>

