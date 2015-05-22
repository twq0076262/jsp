# JSP - HTTP 状态码

HTTP 请求格式和 HTTP 响应消息的格式一样，都有以下结构：

- 一个初始状态行+ CRLF(回车+换行，即新行)

- 零个或多个标题行+ CRLF

- 一个空行，即一个 CRLF

- 一个可选的消息体，像文件，查询数据或查询输出。

例如,一个服务器响应标题看起来如下所示：

<pre>
HTTP/1.1 200 OK
Content-Type: text/html
Header2: ...
...
HeaderN: ...
  (Blank Line)
&lt;!doctype ...&gt;
&lt;html&gt;
&lt;head&gt;...&lt;/head&gt;
&lt;body&gt;
...
&lt;/body&gt;
&lt;/html&gt;
</pre>


状态行包含 HTTP 版本(例子中的 HTTP / 1.1)，状态码(例子中的 200)和对应状态代码的短消息(例子中的 OK)。

下面是 HTTP 状态代码和相关可能从Web服务器返回的消息的一个列表：

<table class="src">
  <tr>
    <th align="left" style="width:10%">编码：</th>
    <th align="left" style="width:30%">消息：</th>
    <th align="left" style="width:60%">描述：</th>
  </tr>
  <tr>
    <td valign="top">100</td><td> Continue</td>
    <td valign="top"> 只有一部分的服务器请求已经收到，但只要没有被拒绝，客户端应该继续请求</td>
  </tr>
  <tr>
    <td valign="top">101</td><td> Switching Protocols</td>
    <td valign="top">服务器交换了协议。 </td>
  </tr>
  <tr>
    <td valign="top">200</td><td> OK</td>
    <td valign="top">请求是 OK</td>
  </tr>
  <tr>
    <td valign="top">201</td><td> Created</td>
    <td valign="top">请求已经完成，新的资源被创建 &nbsp;</td>
  </tr>
  <tr>
    <td valign="top">202</td><td> Accepted</td>
    <td valign="top">请求被接受处理，但是处理还没有完成。 </td>
  </tr>
  <tr>
    <td valign="top">203</td><td style="width:35%;"> Non-authoritative Information</td>
    <td valign="top">&nbsp;</td>
  </tr>
  <tr>
    <td valign="top">204 </td><td>No Content</td>
    <td valign="top">&nbsp; </td>
  </tr>
  <tr>
    <td valign="top">205</td><td> Reset Content</td>
    <td valign="top">&nbsp;</td>
  </tr>
  <tr>
    <td valign="top">206</td><td> Partial Content</td>
    <td valign="top">&nbsp; </td>
  </tr>
  <tr>
    <td valign="top">300</td><td> Multiple Choices</td>
    <td valign="top">一个链接列表。用户可以选择一个链接然后跳转到那个位置。最多可选择 5 个地址 &nbsp;</td>
  </tr>
  <tr>
    <td valign="top">301</td><td> Moved Permanently</td>
    <td valign="top">请求页面已经被移到新的 url 中&nbsp;</td>
  </tr>
  <tr>
    <td valign="top">302</td><td> Found</td>
    <td valign="top">请求页面暂时被移到新的 url 中&nbsp;
    </td>
  </tr>
  <tr>
    <td valign="top">303</td><td> See Other</td>
    <td valign="top">请求页面可在不同的 url 中找到&nbsp;
    </td>
  </tr>
  <tr>
    <td valign="top">304</td><td> Not Modified</td>
    <td valign="top">&nbsp;</td>
  </tr>
  <tr>
    <td valign="top">305</td><td> Use Proxy</td>
    <td valign="top">&nbsp;
    </td>
  </tr>
  <tr>
    <td valign="top">306</td><td> <i>Unused</i></td>
    <td valign="top">该代码是在前一版本使用的。它已不再使用，但该代码保留下来了。</td>
  </tr>
  <tr>
    <td valign="top">307</td><td> Temporary Redirect</td>
    <td valign="top">请求页面被暂时移到新的url中。</td>
  </tr>
   <tr>
    <td valign="top">400</td><td>Bad Request</td>
    <td valign="top">服务器没有理解请求。 </td>
  </tr>
  <tr>
    <td valign="top">401</td><td> Unauthorized</td>
    <td valign="top"> 请求页面需要用户名和密码</td>
  </tr>
  <tr>
    <td valign="top">402</td><td> Payment Required</td>
    <td valign="top"><i>你还不能使用这个代码</i></td>
  </tr>
  <tr>
    <td valign="top">403</td><td> Forbidden</td>
    <td valign="top">不允许访问请求页面 </td>
  </tr>
  <tr>
    <td valign="top">404</td><td> Not Found</td>
    <td valign="top">服务器找不到请求页面。</td>
  </tr>
  <tr>
    <td valign="top">405</td><td> Method Not Allowed</td> 
    <td valign="top">在请求中指定的方法不允许使用。</td>
  </tr>
  <tr>
    <td valign="top">406</td><td> Not Acceptable</td>
    <td valign="top">服务器只能生成一个不被客户端接收的响应。</td>
  </tr>
  <tr>
    <td valign="top">407 </td><td>Proxy Authentication Required</td>
    <td valign="top">在这个请求得到服务之前，你必须验证一个代理服务器。</td>
  </tr>
  <tr>
    <td valign="top">408</td><td> Request Timeout</td>
    <td valign="top">请求花费的时间比服务器准备等待的时间长。 </td>
  </tr>
  <tr>
    <td valign="top">409</td><td> Conflict</td>
    <td valign="top">由于冲突请求不能实现。 </td>
  </tr>
  <tr>
    <td valign="top">410 </td><td>Gone</td>
    <td valign="top">请求页面不再可用。</td>
  </tr>
  <tr>
    <td valign="top">411</td><td> Length Required</td>
    <td valign="top"> &quot;内容-长度&quot; 没有被定义。没有它服务器不会接受请求。</td>
  </tr>
  <tr>
    <td valign="top">412</td><td> Precondition Failed</td>
    <td valign="top">服务器给出给定的请求评估的前提为假。</td>
  </tr>
  <tr>
    <td valign="top">413</td><td> Request Entity Too Large</td>
    <td valign="top">服务器不会接受请求，因为请求实体太大。 </td>
  </tr>
  <tr>
    <td valign="top">414</td><td> Request-url Too Long</td>
    <td valign="top">服务器不会接受请求，因为 url 太长。当你把“post”请求转换为带有很长的查询信息的“get”请求时，这种情况就会发生</td>
  </tr>
  <tr>
    <td valign="top">415</td><td> Unsupported Media Type</td>
    <td valign="top">服务器不会接受请求因为媒体类型不支持。</td>
  </tr>
  <tr>
    <td valign="top">417</td><td> Expectation Failed</td>
    <td valign="top">&nbsp;</td> 
  </tr>
  <tr>
    <td valign="top">500</td><td>Internal Server Error</td>
    <td valign="top">请求未完成。服务器遇到了意外情况。 </td>
  </tr>
  <tr>
    <td valign="top">501</td><td> Not Implemented</td>
    <td valign="top">请求未能完成。服务器不支持所需的功能。</td>
  </tr>
  <tr>
    <td valign="top">502</td><td> Bad Gateway</td>
    <td valign="top">请求未能完成。服务器从上游服务器收到无效响应</td>
  </tr>
  <tr>
    <td valign="top">503</td><td> Service Unavailable</td>
    <td valign="top">请求未能完成。服务器暂时过载或瘫痪。</td>
  </tr>
  <tr>
    <td valign="top">504</td><td> Gateway Timeout</td>
    <td valign="top">网关超时。</td>
  </tr>
  <tr>
    <td valign="top">505</td><td> HTTP Version Not Supported</td>
    <td valign="top">服务器不支持“http 协议”版本。</td>
  </tr>
</table>  

## 设置 HTTP 状态码的方法：

有以下方法可以用来设置 servlet 程序的 HTTP 状态码。有了 HttpServletResponse 对象，这些方法都是可用的。

<table class="table table-bordered">
<tr><th style="width:5%">S.N.</th><th>方法 &amp;描述</th></tr>
<tr><td>1</td><td><p><b>public void setStatus ( int statusCode )</b></p>
<p>此方法设置一个任意的状态码。setStatus 方法接受一个 int(状态码)作为参数。如果你的响应包含一个特殊的状态码和文档，在实际中用 PrintWriter 返回任何内容之前一定要调用 setStatus。</p></td></tr>
<tr><td>2</td><td><p><b>public void sendRedirect(String url)</b></p>
<p>该方法生成一个 302 响应以及一个位置标题给出新文档的 URL。</p></td></tr>
<tr><td>3</td><td><p><b>public void sendError(int code, String message)</b></p>
<p>这种方法发送一个状态码(通常是 404)以及一个在 HTML 文档内自动格式化的短消息并发送到客户端。</p></td></tr>
</table>  

## HTTP 状态码实例：

下面的例子将发送 407 错误代码到客户端浏览器，浏览器将显示“需要验证! ! !”的消息。

<pre class="prettyprint notranslate tryit">
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Setting HTTP Status Code&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;%
   // Set error code and reason.
   response.sendError(407, "Need authentication!!!" );
%&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在调用上述代码，JSP 将显示如下所示的结果：

<pre class="result notranslate">
<h1 style="font-family:Tahoma,Arial,sans-serif;color:white;background-color:#525D76;">HTTP Status 407 - Need authentication!!!</h1>
<p><b style="font-family:Tahoma,Arial,sans-serif;color:white;background-color:#525D76;">type</b> Status report</p>
<p><b style="font-family:Tahoma,Arial,sans-serif;color:white;background-color:#525D76;">message</b> <u>Need authentication!!!</u></p>
<p><b style="font-family:Tahoma,Arial,sans-serif;color:white;background-color:#525D76;">description</b> <u>The client must first authenticate itself with the proxy (Need authentication!!!).</u></p>
<h3 style="font-family:Tahoma,Arial,sans-serif;color:white;background-color:#525D76;">Apache Tomcat/5.5.29</h3>
</pre>
 
想要使用 HTTP 状态代码变得更加舒适，尝试设置不同的状态代码和描述。
