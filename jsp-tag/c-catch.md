# JSTL Core < c:catch > 标签

`<c:catch>` 标签捕获发生在标签主题中的任何异常并有选择地公开它。它仅仅是用于错误处理和更得体地处理这个问题。

## 属性：

`<c:catch>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>var</td><td>保存 java.lang 的变量名。如果抛出的 Throwable 在 body 元素内。</td><td>否</td><td>无</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;c:catch&gt; Tag Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;c:catch var ="catchException"&gt;
   &lt;% int x = 5/0;%&gt;
&lt;/c:catch&gt;

&lt;c:if test = "${catchException != null}"&gt;
   &lt;p&gt;The exception is : ${catchException} &lt;br /&gt;
   There is an exception: ${catchException.message}&lt;/p&gt;
&lt;/c:if&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将会产生如下所示结果：

<pre class="result notranslate">
The exception is : java.lang.ArithmaticException: / by zero
There is an exception: / by zero
</pre>
