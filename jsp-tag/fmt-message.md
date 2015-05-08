# JSTL Core < fmt:message > 标签

`<fmt:message>` 标签将键映射到本地化的消息中并执行参数替换。

## 属性：

`<fmt:message>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>key</td><td>要检索的消息键</td><td>否</td><td>Body</td></tr>
<tr><td>bundle</td><td>使用的资源包</td><td>否</td><td>默认包</td></tr>
<tr><td>var</td><td>存储本地化消息的变量名</td><td>否</td><td>页面输出</td></tr>
<tr><td>scope</td><td>存储本地化消息的变量范围</td><td>否</td><td>页面</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;JSTL fmt:message Tag&lt;/title&gt;
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

这将会生成如下所示结果：

<pre class="result notranslate">
One 
Two 
Three
</pre>
