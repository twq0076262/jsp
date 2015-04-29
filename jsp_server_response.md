# JSP——服务器响应

当一个 Web 服务器响应浏览器的 HTTP 请求时，响应通常包括一个状态行，一些响应标题，一个空行和文档。一个典型的响应如下所示：

<pre class="prettyprint notranslate">
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

下面是最有用的 HTTP 1.1 响应标题的一个总结，它从 web 服务器端回到浏览器，并且在 web 编程时，你会频繁使用它们：

<table class="table table-bordered">
<tr><th style="width:30%">标题</th><th>描述</th></tr>
<tr><td>Allow</td><td>这个标题指定了服务器支持的请求方法(GET、POST 等等)。</td></tr>
<tr><td>Cache-Control</td><td>这个标题指定了响应文档可以安全地被缓存的情况。它可以有<b>public，private</b> 或 <b>non-chche</b> 的值。Public 意味着文件是缓存的，private 意味着文档用于单个用户，且只能存储在私有(非共享)缓存中，non-chche 意味着永远不会被缓存。</td></tr>
<tr><td>Connection</td><td>该标题表明浏览器是否使用持久的HTTP连接。值为 <b>close</b> 表明浏览器不使用持续的 HTTP 连接，<b>keep-alive</b> 表明使用持久连接。</td></tr>
<tr><td>Content-Disposition</td><td>该标题让你请求浏览器要求用户将响应保存到给定名称的磁盘文件中。</td></tr>
<tr><td>Content-Encoding</td><td>这个标题指定了在传输过程中页面被编码的方式。</td></tr>
<tr><td>Content-Language</td><td>这个标题表明了编写文档的语言。例如，英语，美语，俄语等。</td></tr>
<tr><td>Content-Length</td><td>这个标题表明了响应中的字节数。这些信息只有在浏览器使用持久(keep-alive)的HTTP连接时才需要。</td></tr>
<tr><td>Content-Type</td><td>这个标题给出响应文档的 MIME(多用途 Internet 邮件扩展)类型。</td></tr>
<tr><td>Expires</td><td>这个标题指定了内容应该被认为是过时的时间，因此不再被缓存。</td></tr>
<tr><td>Last-Modified</td><td>这个标题表示最后一次修改文档的时间。客户端可以缓存文件并由后面的请求的 if - modified - since 请求标题提供一个日期。 </td></tr>
<tr><td>Location</td><td>这个标题应该包含在所有带有 300 s 状态码的响应中。该标题通知浏览器文档的地址。浏览器自动重新连接到这个位置并且检索新文档。</td></tr>
<tr><td>Refresh</td><td>这个标题指定浏览器应该多久访问更新页面。你可以在页面刷新后，指定时间为几秒。</td></tr>
<tr><td>Retry-After</td><td>这个标题可以与 503(服务不可用)响应结合使用，告诉客户端多久以后它可以重复请求。</td></tr>
<tr><td>Set-Cookie</td><td>这个标题制定了与页面相关联的一个 cookie。</td></tr>
</table>  

## HttpServletResponse 对象

该响应对象是 javax.servlet.http.HttpServletResponse 的一个实例。正如服务器创建请求对象，它也创建了一个对象来表示客户端的响应。

响应对象还定义了接口，处理创建新的 HTTP 标题。通过这个对象 JSP 程序员可以添加新的 cookies 或日期 stamps，HTTP 状态码等。

以下方法可以用来在你的 servlet 程序中设置 HTTP 响应标题。有了代表服务器响应的 HttpServletResponse 对象，这些方法都是可用的。

<table class="table table-bordered">
<tr><th style="width:5%">S.N.</th><th>方法 &amp; 描述</th></tr>
<tr><td>1</td><td><p><b>String encodeRedirectURL(String url)</b></p>
<p>将指定的 URL 编码用于 sendRedirect 方法，如果不需要编码，则返回的 URL 不变。</p></td></tr>
<tr><td>2</td><td><p><b>String encodeURL(String url)</b></p>
<p>编码由包括会话 ID 指定的 URL,或者,如果不需要编码,返回的 URL 不变。</p></td></tr>
<tr><td>3</td><td><p><b>boolean containsHeader(String name)</b></p>
<p>返回一个布尔值表明指定的响应标题是否已经设置。</p></td></tr>
<tr><td>4</td><td><p><b>boolean isCommitted()</b></p>
<p>返回一个布尔值表明响应是否已经提交。 </p></td></tr>
<tr><td>5</td><td><p><b>void addCookie(Cookie cookie)</b></p>
<p>将指定的 cookie 添加到响应中。</p></td></tr>
<tr><td>6</td><td><p><b>void addDateHeader(String name, long date)</b></p>
<p>添加一个带有给定名称和日期值的响应标题。</p></td></tr>
<tr><td>7</td><td><p><b>void addHeader(String name, String value)</b></p>
<p>添加一个带有给定名称和值的响应标题。</p></td></tr>
<tr><td>8</td><td><p><b>void addIntHeader(String name, int value)</b></p>
<p>添加一个带有给定名称和整数值的响应标题。 </p></td></tr>
<tr><td>9</td><td><p><b>void flushBuffer()</b></p>
<p>将缓冲区的内容强行写入到客户端。</p></td></tr>
<tr><td>10</td><td><p><b>void reset()</b></p>
<p>清除缓冲区中的全部数据，以及状态码和标题。</p></td></tr>
<tr><td>11</td><td><p><b>void resetBuffer()</b></p>
<p>清除响应中没有清除头或状态码的潜在的缓冲区的内容。</p></td></tr>
<tr><td>12</td><td><p><b>void sendError(int sc)</b></p>
<p>使用指定的状态代码给客户端发送一个错误响应，并清除缓冲区。</p></td></tr>
<tr><td>13</td><td><p><b>void sendError(int sc, String msg)</b></p>
<p>使用指定的状态给客户端发送一个错误响应。</p></td></tr>
<tr><td>14</td><td><p><b>void sendRedirect(String location)</b></p>
<p>使用指定的重定向位置 URL 给客户端发送一个临时的重定向响应。</p></td></tr>
<tr><td>15</td><td><p><b>void setBufferSize(int size)</b></p>
<p>为响应主体设置首选缓冲区大小。</p></td></tr>
<tr><td>16</td><td><p><b>void setCharacterEncoding(String charset)</b></p>
<p>设置将被发送到客户端的响应的字符编码(MIME字符集)例如 UTF-8。</p></td></tr>
<tr><td>17</td><td><p><b>void setContentLength(int len)</b></p>
<p>设置 HTTP servlet 中的响应的主体内容的长度，这种方法设置了 HTTP 内容-长度标题。</p></td></tr>
<tr><td>18</td><td><p><b>void setContentType(String type)</b></p>
<p>如果响应尚未提交，设置要被发送到客户端的响应的内容类型。</p></td></tr>
<tr><td>19</td><td><p><b>void setDateHeader(String name, long date)</b></p>
<p>用给定的名称和日期值设置一个响应标题。</p></td></tr>
<tr><td>20</td><td><p><b>void setHeader(String name, String value)</b></p>
<p> 用给定的名称和值设置一个响应标题。</p></td></tr>
<tr><td>21</td><td><p><b>void setIntHeader(String name, int value)</b></p>
<p>用给定的名称和整数值设置一个响应标题。</p></td></tr>
<tr><td>22</td><td><p><b>void setLocale(Locale loc)</b></p>
<p>如果反应尚未提交，设置响应的语言环境。</p></td></tr>
<tr><td>23</td><td><p><b>void setStatus(int sc)</b></p>
<p>为响应设置状态码。 </p></td></tr>
</table>  

## HTTP 标题响应实例：

接下来的例子中将使用 **setIntHeader()**方法设置 **Refresh** 标题来模拟数字时钟：

<pre class="prettyprint notranslate tryit">
&lt;%@ page import="java.io.*,java.util.*" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Auto Refresh Header Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h2&gt;Auto Refresh Header Example&lt;/h2&gt;
&lt;%
   // Set refresh, autoload time as 5 seconds
   response.setIntHeader("Refresh", 5);
   // Get current time
   Calendar calendar = new GregorianCalendar();
   String am_pm;
   int hour = calendar.get(Calendar.HOUR);
   int minute = calendar.get(Calendar.MINUTE);
   int second = calendar.get(Calendar.SECOND);
   if(calendar.get(Calendar.AM_PM) == 0)
      am_pm = "AM";
   else
      am_pm = "PM";
   String CT = hour+":"+ minute +":"+ second +" "+ am_pm;
   out.println("Current Time is: " + CT + "\n");
%&gt;
&lt;/center&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在把上面的代码添加到 main.jsp 并试图访问它。这将在每5秒后显示当前系统时间如下所示。运行 JSP，等着看结果： 

<pre class="result notranslate">
<center>
<h2 align="center">Auto Refresh Header Example</h2>
Current Time is: 9:44:50 PM
</center>
</pre>


想要变得更加舒适你可以以相同的方式试试上面几个方法。
