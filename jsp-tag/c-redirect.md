# JSTL Core < c:redirect > 标签

`<c:redirect>` 标签通过提供自动 URL 重写，将浏览器重定向到另一个 URL，它支持上下文相关的 URL，支持 `<c:param>` 标签。

## 属性

`<c:redirect>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>url</td><td>重定向到用户浏览器的 URL</td><td>是</td><td>无</td></tr>
<tr><td>context</td><td>/ 紧随其后的是一个本地 web 应用程序</td><td>无</td><td style="width:25%;">当前应用程序</td></tr>
</table>

## 实例：

如果你需要传递参数到 <c:import> 标签，首先使用 <c:url> 标签创建 URL，如下所示：

<pre class="prettyprint notranslate">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;c:redirect&gt; Tag Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;c:redirect url="http://www.photofuntoos.com"/&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

上述例子会重定向请求到 http://www.photofuntoos.com——你可以自己尝试一下。