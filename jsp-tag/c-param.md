# JSTL Core < c:param > 标签

< c:param > 标签允许 URL 指定适当的 URL 请求参数，且允许任何必要的 URL 编码要求。


在 < c:param > 标签内 name 属性表示参数名称，value 属性显示参数值:

## 属性：

< c:param > 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>name</td><td>在 URL 中设置的请求参数的名称</td><td>是</td><td>无</td></tr>
<tr><td>value</td><td>在 URL 中设置的请求参数的值</td><td>否</td><td>Body</td></tr>
</table>

## 实例：

如果你需要传递参数给 <c:param> 标签，首先使用 <c:url> 标签来创建 URL，如下所示：

``` 
<c:url value="/index.jsp" var="myURL">
   <c:param name="trackingId" value="1234"/>
   <c:param name="reportType" value="summary"/>
</c:url>
<c:import url="${myURL}"/>
```

上述请求会传递给 URL，如下所示——你可以尝试一下。

<pre class="prettyprint notranslate">
"/index.jsp?trackingId=1234;reportType=summary"
</pre>

