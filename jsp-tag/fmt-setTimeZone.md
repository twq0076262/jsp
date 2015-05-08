# JSTL Core < fmt:setTimeZone > 标签

`<fmt:setTimeZone>` 标签用于将时区对象复制到指定的范围变量中。

## 属性：

`<fmt:setTimeZone>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>value</td><td>作为给定范围的变量或配置变量显示的时区</td><td>是</td><td>无</td></tr>
<tr><td>var</td><td>存储新时区的变量名</td><td>否</td><td>取代默认值</td></tr>
<tr><td>scope</td><td>存储新时区的变量范围</td><td>否</td><td>页面</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;JSTL fmt:setTimeZone Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;c:set var="now" value="&lt;%=new java.util.Date()%&gt;" /&gt;
&lt;p&gt;Date in Current Zone: &lt;fmt:formatDate value="${now}" 
             type="both" timeStyle="long" dateStyle="long" /&gt;&lt;/p&gt;
&lt;p&gt;Change Time Zone to GMT-8&lt;/p&gt;
&lt;fmt:setTimeZone value="GMT-8" /&gt;
&lt;p&gt;Date in Changed Zone: &lt;fmt:formatDate value="${now}" 
             type="both" timeStyle="long" dateStyle="long" /&gt;&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示的结果：

<pre class="result notranslate">
<p>Date in Current Zone: 23 September 2010 15:21:37 GST</p>
<p>Change Time Zone to GMT-8</p>
<p>Date in Changed Zone: 23 September 2010 03:21:37 GMT-08:00</p>
</pre>
