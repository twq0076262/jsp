# JSTL Core < c:set > 标签

< c:set > 标签是 setProperty 操作的 JSTL-友好版本。该标签非常有用，因为它计算表达式并使用计算结果来设置 JavaBean 或 java.util.Map 对象的值。

## 属性：

< c:set > 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>value</td><td>保存的信息</td><td>否</td><td>主体</td></tr>
<tr><td>target</td><td>属性被修改的变量名称</td><td>否</td><td>无</td></tr>
<tr><td>property</td><td>修改的属性</td><td>否</td><td>无</td></tr>
<tr><td>var</td><td>存储信息的变量名称</td><td>否</td><td>无</td></tr>
<tr><td>scope</td><td>存储信息的变量范围</td><td>否</td><td>页面</td></tr>
</table>

如果指定了目标，那么属性也一定被指定。

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;c:set&gt; Tag Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;c:set var="salary" scope="session" value="${2000*2}"/&gt;
&lt;c:out value="${salary}"/&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

这将会产生如下所示结果：

<pre class="result notranslate">
4000
</pre>

