# JSTL Core < c:choose >, < c:when >, < c:otherwise > 标签

< c:choose > 就像 Java **switch** 语句，它可以让你进行一些选择。正如 **switch** 语句有 **case** 语句，<c:choose> 标签有 <c:when> 标签。一个 switch 语句中有 **default** 子句来指定一个默认的操作，同样的方式<c:choose>有<c:otherwise>作为默认子句。

## 属性: 

- < c:choose > 标签没有任何属性。

- < c:when > 标签有一个属性，在下面列出了。

- < c:otherwise > 标签没有任何属性。

< c:when > 标签具有以下属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>test</td><td>计算的条件</td><td>是</td><td>无</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;c:choose&gt; Tag Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;c:set var="salary" scope="session" value="${2000*2}"/&gt;
&lt;p&gt;Your salary is : &lt;c:out value="${salary}"/&gt;&lt;/p&gt;
&lt;c:choose&gt;
    &lt;c:when test="${salary &lt;= 0}"&gt;
       Salary is very low to survive.
    &lt;/c:when&gt;
    &lt;c:when test="${salary &gt; 1000}"&gt;
        Salary is very good.
    &lt;/c:when&gt;
    &lt;c:otherwise&gt;
        No comment sir...
    &lt;/c:otherwise&gt;
&lt;/c:choose&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
Your salary is : 4000
Salary is very good. 
</pre>
