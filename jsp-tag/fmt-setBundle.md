# JSTL Core < fmt:setBundle > 标签

`<fmt:setBundle>` 标签用于加载资源包，并把它存储在已命名的给定范围的变量中或存储在包配置变量中。

## 属性：

`<fmt:setBundle>` 标签具有如下所示属性：

<table class="src">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>basename</td><td>资源包家族的基本名称，作为一个给定范围的变量或配置变量来显示</td><td>是</td><td>无</td></tr>
<tr><td>var</td><td>存储新包的变量名</td><td>否</td><td>取代默认值</td></tr>
<tr><td>scope</td><td>存储新包的变量范围</td><td>否</td><td>页面</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;JSTL fmt:setBundle Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;fmt:setLocale value="en"/&gt;
&lt;fmt:setBundle basename="com.tutorialspoint.Example" var="lang"/&gt;

&lt;fmt:message key="count.one" bundle="${lang}"/&gt;&lt;br/&gt;
&lt;fmt:message key="count.two" bundle="${lang}"/&gt;&lt;br/&gt;
&lt;fmt:message key="count.three" bundle="${lang}"/&gt;&lt;br/&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
One 
Two 
Three
</pre>
