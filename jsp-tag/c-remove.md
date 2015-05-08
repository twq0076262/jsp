# JSTL Core < c:remove > 标签

`<c:remove>` 标签从指定的范围或变量被发现的首个范围中(如果没有指定范围)删除变量。该操作通常并不是特别有用，但是它可以帮助确保 JSP 清理任何 JSP 负责的限定作用域资源。

## 属性：

`<c:remove>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>var</td><td>要删除的变量名称</td><td>是</td><td>无</td></tr>
<tr><td>scope</td><td>要删除的变量范围</td><td>否</td><td>全部范围</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;c:remove&gt; Tag Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;c:set var="salary" scope="session" value="${2000*2}"/&gt;
&lt;p&gt;Before Remove Value: &lt;c:out value="${salary}"/&gt;&lt;/p&gt;
&lt;c:remove var="salary"/&gt;
&lt;p&gt;After Remove Value: &lt;c:out value="${salary}"/&gt;&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

这将会产生如下所示结果：

<pre class="result notranslate">
Before Remove Value: 4000
After Remove Value: 
</pre>
