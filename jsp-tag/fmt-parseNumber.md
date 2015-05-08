# JSTL Core < fmt:parseNumber > 标签

`<fmt:parseNumber>` 标签用于解析数字、百分比和货币。

## 属性：

`<fmt:parseNumber>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>value</td><td>要读取（解析）的数值</td><td>否</td><td>Body</td></tr>
<tr><td>type</td><td>数字、货币或百分比</td><td>否</td><td>数字</td></tr>
<tr><td>parseLocale</td><td>解析数字时使用的语言环境</td><td>否</td><td>默认语言环境</td></tr>
<tr><td>integerOnly</td><td>解析一个整数（true）还是解析一个浮点数（false）</td><td>否</td><td>false</td></tr>
<tr><td>pattern</td><td>自定义解析模式</td><td>否</td><td>无</td></tr>
<tr><td>timeZone</td><td>显示日期的时区</td><td>否</td><td>默认的时区</td></tr>
<tr><td>var</td><td>存储解析数字的变量名</td><td>否</td><td>页面输出</td></tr>
<tr><td>scope</td><td>存储格式化数字的变量范围</td><td>否</td><td>页面</td></tr>
</table>

提供的 pattern 属性的工作方式与 < fmt:formatNumber > 标签的 pattern 属性类似。然而，在解析的情况中，pattern 属性告诉解析器想要什么格式。

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %&gt;
&lt;%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %&gt;

&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;JSTL fmt:parseNumber Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;h3&gt;Number Parsing:&lt;/h3&gt;
&lt;c:set var="balance" value="1250003.350" /&gt;

&lt;fmt:parseNumber var="i" type="number" value="${balance}" /&gt;
&lt;p&gt;Parsed Number (1) : &lt;c:out value="${i}" /&gt;&lt;/p&gt;
&lt;fmt:parseNumber var="i" integerOnly="true" 
                       type="number" value="${balance}" /&gt;
&lt;p&gt;Parsed Number (2) : &lt;c:out value="${i}" /&gt;&lt;/p&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将会产生如下所示结果：


<pre class="result notranslate">
<h3>Number Parsing:</h3>
<p>Parsed Number (1) : 1250003.35</p>
<p>Parsed Number (2) : 1250003</p>
</pre>
