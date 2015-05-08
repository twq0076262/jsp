# JSTL Core < c:if > 标签

< c:if > 标签计算表达式，当且仅当表达式的值为真时，显示其主体内容。

## 属性：

< c:if > 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>test</td><td>计算的条件</td><td>是</td><td>无</td></tr>
<tr><td>var</td><td>存储条件结果的变量名</td><td>否</td><td>无</td></tr>
<tr><td>scope</td><td>存储条件结果的变量范围</td><td>否</td><td>页面</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;c:if&gt; Tag Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;c:set var="salary" scope="session" value="${2000*2}"/&gt;
&lt;c:if test="${salary &gt; 2000}"&gt;
   &lt;p&gt;My salary is: &lt;c:out value="${salary}"/&gt;&lt;p&gt;
&lt;/c:if&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

这将会产生如下所示结果：

<pre class="result notranslate">
My salary is: 4000
</pre>

