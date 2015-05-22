# JSP - 客户端请求

当浏览器请求一个网页时，它向 web 服务器发送大量的信息，信息不能直接阅读，因为这些信息作为 HTTP 请求标题的一部分行进。关于这点你可以查看 [**HTTP Protocol**](http://wiki.jikexueyuan.com.com/project/http/) 来了解更多的信息。

以下是来自浏览器端的重要的标题，在网络编程中你将会频繁的使用：

<table class="table table-bordered">
<tr><th style="width:30%">标题</th><th>描述</th></tr>
<tr><td>Accept</td><td>该标题指定了浏览器或其他客户可以处理的 MIME 类型。<b>image/png</b> 或 <b>image/jpeg</b> 的值是两种最常见的可能性。</td></tr>
<tr><td>Accept-Charset</td><td>该标题指定了浏览器可以用来显示信息的字符集。例如 iso - 8859 - 1。</td></tr>
<tr><td>Accept-Encoding</td><td>这个标题指定了浏览器知道如何处理的编码类型。<b>gzip</b> 或 <b>compressare</b> 的值是两种最常见的可能性。</td></tr>
<tr><td>Accept-Language</td><td>这个标题指定客户的首选语言，以防 servlet 可以产生多个语言的结果。例如英语，美语，俄语等。</td></tr>
<tr><td>Authorization</td><td>这个标题是客户访问密码保护的 Web 页面时用来识别他们自己的。</td></tr>
<tr><td>Connection</td><td>这个标题表明客户端是否能处理持续的 HTTP 连接。持续连接允许客户端或其他浏览器用单个请求检索多个文件。<b>Keep-Alive</b> 的值意味着应该使用持续连接</td></tr>
<tr><td>Content-Length</td><td>该标题只适用于 POST 请求和以字节形式给出 POST 数据的大小。 </td></tr>
<tr><td>Cookie</td><td>这个标题为之前发送它们到浏览器的服务器返回 cookies。</td></tr>
<tr><td>Host</td><td>这个标题指定主机和端口正如原始URL给出的一样。</td></tr>
<tr><td>If-Modified-Since</td><td>这个标题表明，客户只想得到在指定日期后更改的页面。服务器发送一个代码，304 意味着 <b>没有</b> 修改标题如果没有更新的结果是可用的。</td></tr>
<tr><td>If-Unmodified-Since</td><td>这个标题的作用与 if - modified – since 是相反的；它指定当且仅当文档比指定的日期要早时，操作应该成功。</td></tr>
<tr><td>Referer</td><td>这个标题表示了引用的 Web 页面的 URL。例如，如果你在 Web 页面 1，点击一个链接到 Web 页面 2，当浏览器请求 Web 页面 2 时，web 页面 1 的 URL 是包含在引用标题中的。</td></tr>
<tr><td>User-Agent</td><td>这个标题标识浏览器或其他做出请求的客户，对应不同类型的浏览器可以返回不同的内容。</td></tr>
</table> 

## HttpServletRequest 对象

该请求对象是 javax.servlet.http. HttpServletRequest 对象的一个实例。每次客户端请求一个页面时，JSP 引擎就会创建一个新的对象来表示这个请求。

请求对象提供方法来获取 HTTP 标题信息，包括表单数据，cookies，HTTP 方法等。

有以下重要的方法可用于读取 JSP 程序中的 HTTP 标题。有了 HttpServletRequest 对象，这些方法都可用的，该对象代表客户端对网络服务器的请求。

<table class="table table-bordered">
<tr><th style="width:5%">S.N.</th><th>方法 &amp; 描述</th></tr>
<tr><td>1</td><td><p><b>Cookie[] getCookies()</b></p>
<p>返回一个数组，其中包含客户端用这个请求发送的所有 Cookie 对象。</p></td></tr>
<tr><td>2</td><td><p><b>Enumeration getAttributeNames()</b></p>
<p>返回一个枚举包含此请求可用的属性的名称。</p></td></tr>
<tr><td>3</td><td><p><b>Enumeration getHeaderNames()</b></p>
<p>返回一个这个请求包含的所有标题名称的枚举。</p></td></tr>
<tr><td>4</td><td><p><b>Enumeration getParameterNames()</b></p>
<p>返回一个字符串对象的枚举，该字符串对象包括包含在此请求中的参数的名称。</p></td></tr>
<tr><td>5</td><td><p><b>HttpSession getSession()</b></p>
<p>返回与此请求相关的当前会话，或者如果该请求没有会话，那么就创建一个。</p></td></tr>
<tr><td>6</td><td><p><b>HttpSession getSession(boolean create)</b></p>
<p>返回与这个请求相关的当前的HttpSession或，如果没有当前会话并且 create 为真，那么返回一个新的会话。</p></td></tr>
<tr><td>7</td><td><p><b>Locale getLocale()</b></p>
<p>返回客户会接受内容的首选区域设置，基于所包含的 accept – language 标题</p></td></tr>
<tr><td>8</td><td><p><b>Object getAttribute(String name)</b></p>
<p>作为一个对象返回指定属性的值，如果指定的名称没有属性，返回 null。</p></td></tr>
<tr><td>9</td><td><p><b>ServletInputStream getInputStream()</b></p>
<p>使用 ServletInputStream 将请求的主体作为二进制数据检索。</p></td></tr>
<tr><td>10</td><td><p><b>String getAuthType()</b></p>
<p>返回用于保护 servlet 的验证方案的名称，例如，“BASIC”或“SSL”，如果 JSP 没有被保护，那么返回 null</p></td></tr>
<tr><td>11</td><td><p><b>String getCharacterEncoding()</b></p>
<p>返回在该请求内部使用的字符编码的名称。</p></td></tr>
<tr><td>12</td><td><p><b>String getContentType()</b></p>
<p> 返回该请求主体的 MIME 类型，如果不知道类型，返回 null。</p></td></tr>
<tr><td>13</td><td><p><b>String getContextPath()</b></p>
<p>返回表示请求上下文的请求 URI 的一部分。</p></td></tr>
<tr><td>14</td><td><p><b>String getHeader(String name)</b></p>
<p>将指定的请求标题的值作为一个字符串返回。</p></td></tr>
<tr><td>15</td><td><p><b>String getMethod()</b></p><p>返回生成该请求的 HTTP 方法的名称，比如 GET，POST，或 PUT。</p></td></tr>
<tr><td>16</td><td><p><b>String getParameter(String name)</b></p>
<p>将一个请求参数的值作为字符串返回，如果参数不存在，返回 null。</p></td></tr>
<tr><td>17</td><td><p><b>String getPathInfo()</b></p>
<p>返回与客户端生成请求时发送的 URL 相关联的任何额外的路径信息。</p></td></tr>
<tr><td>18</td><td><p><b>String getProtocol()</b></p>
<p>返回请求协议的名称和版本。</p></td></tr>
<tr><td>19</td><td><p><b>String getQueryString()</b></p>
<p>返回在路径后包含在请求 URL 的查询字符串。</p></td></tr>
<tr><td>20</td><td><p><b>String getRemoteAddr()</b></p>
<p>返回发送请求的客户端的互联网协议(IP)地址。</p></td></tr>
<tr><td>21</td><td><p><b>String getRemoteHost()</b></p>
<p>返回发送请求的客户机的全称。</p></td></tr>
<tr><td>22</td><td><p><b>String getRemoteUser()</b></p>
<p>如果用户已经通过身份验证，就返回发出这一请求的登录用户，如果用户没有被验证，那么返回 null。</p></td></tr>
<tr><td>23</td><td><p><b>String getRequestURI()</b></p>
<p>从取决于 HTTP 请求首行的查询字符串的协议名称中返回请求 URL 的一部分。</p></td></tr>
<tr><td>24</td><td><p><b>String getRequestedSessionId()</b></p>
<p>返回客户端指定的会话 ID。 </p></td></tr>
<tr><td>25</td><td><p><b>String getServletPath()</b></p>
<p>返回调用 JSP 的请求 URL 的部分。</p></td></tr>
<tr><td>26</td><td><p><b>String[] getParameterValues(String name)</b></p>
<p>返回一个字符串对象数组，其中包含所有的给定的请求参数的值，如果参数不存在，那么返回 null。</p></td></tr>
<tr><td>27</td><td><p><b>boolean isSecure()</b></p>
<p>返回一个布尔值表示是否使用一个安全通道发出了这个请求，比如 HTTPS。</p></td></tr>
<tr><td>28</td><td><p><b>int getContentLength()</b></p>
<p>以字节为单位，返回请求的主体长度并通过输入流使其可用，如果长度是未知的，那么返回 -1。</p></td></tr>
<tr><td>29</td><td><p><b>int getIntHeader(String name)</b></p>
<p>作为 int 返回指定请求标题的值。</p></td></tr>
<tr><td>30</td><td><p><b>int getServerPort()</b></p>
<p>返回收到这个请求的端口号。</p></td></tr>
</table> 

## HTTP 标题请求实例

下面是使用 HttpServletRequest 的 **getHeaderNames()** 方法读取 HTTP 标题信息的实例。该方法返回一个枚举，包含与当前 HTTP 请求相关的标题信息。

一旦得到一个枚举，我们可以以标准的方式循环枚举，使用 *hasMoreElements()* 方法来确定何时停止，使用 *nextElement()* 方法得到每个参数的名字。

<pre class="prettyprint notranslate">
&lt;%@ page import="java.io.*,java.util.*" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;HTTP Header Request Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h2&gt;HTTP Header Request Example&lt;/h2&gt;
&lt;table width="100%" border="1" align="center"&gt;
&lt;tr bgcolor="#949494"&gt;
&lt;th&gt;Header Name&lt;/th&gt;&lt;th&gt;Header Value(s)&lt;/th&gt;
&lt;/tr&gt;
&lt;%
   Enumeration headerNames = request.getHeaderNames();
   while(headerNames.hasMoreElements()) {
      String paramName = (String)headerNames.nextElement();
      out.print("&lt;tr&gt;&lt;td&gt;" + paramName + "&lt;/td&gt;\n");
      String paramValue = request.getHeader(paramName);
      out.println("&lt;td&gt; " + paramValue + "&lt;/td&gt;&lt;/tr&gt;\n");
   }
%&gt;
&lt;/table&gt;
&lt;/center&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在把上述代码添加到 main.jsp 中并试图访问它。这将产生的如下所示的结果：

## HTTP 标题请求实例

<table width="100%" border="1" align="center" class="table table-bordered">
<tr bgcolor="#949494">
<th width="30%">标题名称</th><th>标题值</th>
</tr>
<tr><td>accept</td>
<td>*/*</td></tr>
<tr><td>accept-language</td>
<td>en-us</td></tr>
<tr><td>user-agent</td>
<td>Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; Trident/4.0; InfoPath.2; MS-RTC LM 8)</td></tr>
<tr><td>accept-encoding</td>
<td>gzip, deflate</td></tr>
<tr><td>host</td>
<td>localhost:8080</td></tr>
<tr><td>connection</td>
<td>Keep-Alive</td></tr>
<tr><td>cache-control</td>
<td>no-cache</td></tr>
</table>  

想要用其他方法变得更加舒服，你可以用相同的方法试试上面列出的几个方法。
