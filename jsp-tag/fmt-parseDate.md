# JSTL Core < fmt:parseDate > 标签

< fmt:parseDate > 标签用于解析日期。

## 属性：

< fmt:parseDate > 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>value</td><td>要读取（解析）的日期值</td><td>否</td><td>Body</td></tr>
<tr><td>type</td><td>日期、时间或两者</td><td>否</td><td>日期</td></tr>
<tr><td>dateStyle</td><td>FULL, LONG, MEDIUM, SHORT, 或默认</td><td>否</td><td>默认</td></tr>
<tr><td>timeStyle</td><td>FULL, LONG, MEDIUM, SHORT, 或默认</td><td>否</td><td>默认</td></tr>
<tr><td>parseLocale</td><td>解析日期时使用的语言环境</td><td>否</td><td>默认语言环境</td></tr>
<tr><td>pattern</td><td>自定义解析模式</td><td>否</td><td>无</td></tr>
<tr><td>timeZone</td><td>解析的日期的时区</td><td>否</td><td>默认的时区</td></tr>
<tr><td>var</td><td>存储解析日期的变量名</td><td>否</td><td>页面输出</td></tr>
<tr><td>scope</td><td>存储格式化日期的变量范围</td><td>否</td><td>页面</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %&gt;
&lt;%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %&gt;

&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;JSTL fmt:parseDate Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;h3&gt;Date Parsing:&lt;/h3&gt;
&lt;c:set var="now" value="20-10-2010" /&gt;

&lt;fmt:parseDate value="${now}" var="parsedEmpDate" 
                              pattern="dd-MM-yyyy" /&gt;
&lt;p&gt;Parsed Date: &lt;c:out value="${parsedEmpDate}" /&gt;&lt;/p&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示的结果：

<pre class="result notranslate">
<h3>Date Parsing:</h3>
<p>Parsed Date: Wed Oct 20 00:00:00 GST 2010</p>
</pre>
