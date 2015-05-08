# JSTL Core < c:import > 标签

`<c:import>` 标签提供了 `<include>` 操作的所有的功能，同时也可以包含绝对URL。

例如，使用 import 标签允许包含来自不同的 Web 站点或 FTP 服务器的内容。

## 属性: 

`<c:import>`标签具有以下属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>url</td><td>检索和导入到页面的 URL</td><td>是</td><td>无</td></tr>
<tr><td>context</td><td>/ 紧随其后的是本地的一个web应用程序的名称</td><td>否</td><td>当前应用程序</td></tr>
<tr><td>charEncoding</td><td> 为导入数据使用的字符集</td><td>否</td><td>ISO-8859-1</td></tr>
<tr><td>var</td><td>存储导入文本的变量名</td><td>否</td><td>页面输出</td></tr>
<tr><td>scope</td><td>存储导入文本的变量范围</td><td>否</td><td>页面</td></tr>
<tr><td>varReader</td><td>显示 java.io.Reader 的另一个变量的名称</td><td>否</td><td>无</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;c:import&gt; Tag Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;c:import var="data" url="http://www.tutorialspoint.com"/&gt;
&lt;c:out value="${data}"/&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

上面的例子将从 tutorialspoint.com/index.htm 获取完整的内容,这将存储在变量数据中并最终输出出来。你可以自己尝试一下。

