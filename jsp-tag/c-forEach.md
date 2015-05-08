# JSTL Core < c:forEach >, < c:forTokens > 标签

这些标签是通过一个小脚本嵌入 Java **for**，**while** 或 **do-while** 循环的不错的选择。`<c:forEach>` 标签更常用的标签，因为它遍历一个对象集合。`<c:forTokens>` 标签用于将一个字符串分成 token 并遍历每个 token。

## 属性：

`<c:forEach>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>items</td><td>遍历的信息</td><td>否</td><td>无</td></tr>
<tr><td>begin</td><td>开始的元素 (0 = 第一个项目, 1 = 第二个项目, ...)</td><td>否</td><td>0</td></tr>
<tr><td>end</td><td>结束的元素 (0 = 第一个项目, 1 = 第二个项目, ...)</td><td>否</td><td>最后一个元素</td></tr>
<tr><td>step</td><td>处理每一步的元素</td><td>否</td><td>1</td></tr>
<tr><td>var</td><td>显示当前项目的变量名</td><td>否</td><td>无</td></tr>
<tr><td>varStatus</td><td>显示循环状态的变量名</td><td>否</td><td>无</td></tr>
</table>

<c:forTokens> 标签与 <c:forEach> 标签具有相同的属性，另外 <c:forTokens> 标签有一个额外的属性 **delims** 指定了用作分隔符的符号。

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>delims</td><td>用作分隔符的符号</td><td>是</td><td>无</td></tr>
</table>

## <c:forEach> 的实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;c:forEach&gt; Tag Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;c:forEach var="i" begin="1" end="5"&gt;
   Item &lt;c:out value="${i}"/&gt;&lt;p&gt;
&lt;/c:forEach&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
Item 1
Item 2
Item 3
Item 4
Item 5
</pre>

## <c:forTokens> 的实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;c:forTokens&gt; Tag Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;c:forTokens items="Zara,nuha,roshy" delims="," var="name"&gt;
   &lt;c:out value="${name}"/&gt;&lt;p&gt;
&lt;/c:forTokens&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
Zara
nuha
roshy
</pre>
