# JSP——会话跟踪

HTTP 是一个“无状态”协议，这意味着每一次客户端检索 Web 页面时，客户端打开一个单独的 Web 服务器且服务器不会自动连接任何以前的客户端请求的记录。

Web 客户端和 web 服务器之间的会话有以下三种方式：

## Cookies：

网络服务器可以为每个 web 客户端和使用已接收的 cookie 可识别的来自客户端的后续请求分配一个唯一的会话 ID 作为 cookie。

这可能不是一个有效的方法，因为许多时间浏览器不支持 cookie，所以我不建议使用这个过程来维护会话。

## 隐藏的表单字段：

一个 web 服务器可以发送一个隐藏的 HTML 表单字段以及一个独特的会话 ID，如下所示：

``` 
<input type="hidden" name="sessionid" value="12345">
```

这个条目意味着，提交表单时，指定的名称和值会自动包含在 GET 或 POST 数据中。每次当 web 浏览器发送回请求时，session_id 的值可以用来跟踪不同的 web 浏览器。

这可能是跟踪会话的一个有效的方式，但点击一个常规的(< a HREF…>)超文本链接不会引起表单提交，所以隐藏表单字段也不能支持通用会话跟踪。

## URL重写：

你可以在每个识别会话的 URL 结尾添加一些额外的数据，且服务器可以用它存储的关于会话的数据与会话标识符关联起来。

例如，http://tutorialspoint.com/file.htm;sessionid = 12345，会话标识符作为 sessionid = 12345 附加，也可以在web服务器访问来识别客户端。

当它们不支持 cookie 时，URL 重写是维持会话和适用于浏览器的一个更好的方法，但缺点是尽管页面是简单的静态 HTML 页面，但需要动态的生成每个URL来分配一个会话 ID。

## 会话对象：

除了上面提到的三种方法，JSP 使用 servlet 提供的 HttpSession 接口，该接口提供了一种方法来识别网站中跨多个页面请求或访问的用户，并存储用户信息。

默认情况下，JSP 为每个新的客户端自动的启用会话跟踪和一个新的被实例化的 HttpSession 对象。禁用会话跟踪需要通过设置页面指令会话属性为 false 显式地关闭它，如下所示：

``` 
<%@ page session="false" %>
```

JSP 引擎通过隐式的 **session** 对象暴露了 HttpSession 对象给 JSP 开发人员。由于**会话**对象已经提供给 JSP 程序员，程序员可以立即从对象中开始存储和检索数据，不需要任何初始化或 getSession()。

这是会话对象的可用的重要方法的一个总结：

<table class="table table-bordered">
<tr><th style="width:5%">S.N.</th><th>方法 &amp; 描述</th></tr>
<tr><td>1</td><td><b>public Object getAttribute(String name)</b><br />该方法返回会话中与指定的名称绑定的对象，如果没有绑定对象名称，返回 null。</td></tr>
<tr><td>2</td><td><b>public Enumeration getAttributeNames()</b><br />该方法返回一个字符串对象的枚举，其中包含绑定到这个会话的所有对象的名字。</td></tr>
<tr><td>3</td><td><b>public long getCreationTime()</b><br />该方法返回创建会话的时间，自GMT时间1970年1月1日凌晨以来，以毫秒为单位。</td></tr>
<tr><td>4</td><td><b>public String getId()</b><br />该方法返回一个字符串，其中包含分配给这个会话的唯一标识符。</td></tr>
<tr><td>5</td><td><b>public long getLastAccessedTime()</b><br />该方法返回上次客户端发送与这个会话相关的请求的时间，自GMT时间1970年1月1日凌晨以来，毫秒的数量。</td></tr>
<tr><td>6</td><td><b>public int getMaxInactiveInterval()</b><br />该方法返回最大时间间隔，以秒为单位，servlet 容器在客户端访问中将打开这个会话。</td></tr>
<tr><td>7</td><td><b>public void invalidate()</b><br />这个方法使会话无效并解除全部绑定到该会话的对象。</td></tr>
<tr><td>8</td><td><b>public boolean isNew(</b><br />如果客户端还不知道会话或如果客户选择不加入会话，这个方法返回 true。</td></tr>
<tr><td>9</td><td><b>public void removeAttribute(String name)</b><br />该方法从会话中删除制定名称的绑定对象。 </td></tr>
<tr><td>10</td><td><b>public void setAttribute(String name, Object value) </b><br />该方法使用指定的名称解除会话的一个对象。</td></tr>
<tr><td>11</td><td><b>public void setMaxInactiveInterval(int interval)</b><br />在 servlet 容器使这个会话无效之前，这种方法在客户端请求之间指定了时间，以秒为单位，。</td></tr>
</table> 
## 会话跟踪示例：

这个例子描述了如何使用 HttpSession 对象发现一个会话的创建时间和上次访问时间。如果会话不存在，我们将会使请求与一个新的会话相关联。

<pre class="prettyprint notranslate">
&lt;%@ page import="java.io.*,java.util.*" %&gt;
&lt;%
   // Get session creation time.
   Date createTime = new Date(session.getCreationTime());
   // Get last access time of this web page.
   Date lastAccessTime = new Date(session.getLastAccessedTime());

   String title = "Welcome Back to my website";
   Integer visitCount = new Integer(0);
   String visitCountKey = new String("visitCount");
   String userIDKey = new String("userID");
   String userID = new String("ABCD");

   // Check if this is new comer on your web page.
   if (session.isNew()){
      title = "Welcome to my website";
      session.setAttribute(userIDKey, userID);
      session.setAttribute(visitCountKey,  visitCount);
   } 
   visitCount = (Integer)session.getAttribute(visitCountKey);
   visitCount = visitCount + 1;
   userID = (String)session.getAttribute(userIDKey);
   session.setAttribute(visitCountKey,  visitCount);
%&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Session Tracking&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;Session Tracking&lt;/h1&gt;
&lt;/center&gt;
&lt;table border="1" align="center"&gt; 
&lt;tr bgcolor="#949494"&gt;
   &lt;th&gt;Session info&lt;/th&gt;
   &lt;th&gt;Value&lt;/th&gt;
&lt;/tr&gt; 
&lt;tr&gt;
   &lt;td&gt;id&lt;/td&gt;
   &lt;td&gt;&lt;% out.print( session.getId()); %&gt;&lt;/td&gt;
&lt;/tr&gt; 
&lt;tr&gt;
   &lt;td&gt;Creation Time&lt;/td&gt;
   &lt;td&gt;&lt;% out.print(createTime); %&gt;&lt;/td&gt;
&lt;/tr&gt; 
&lt;tr&gt;
   &lt;td&gt;Time of Last Access&lt;/td&gt;
   &lt;td&gt;&lt;% out.print(lastAccessTime); %&gt;&lt;/td&gt;
&lt;/tr&gt; 
&lt;tr&gt;
   &lt;td&gt;User ID&lt;/td&gt;
   &lt;td&gt;&lt;% out.print(userID); %&gt;&lt;/td&gt;
&lt;/tr&gt; 
&lt;tr&gt;
   &lt;td&gt;Number of visits&lt;/td&gt;
   &lt;td&gt;&lt;% out.print(visitCount); %&gt;&lt;/td&gt;
&lt;/tr&gt; 
&lt;/table&gt; 
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在将上述代码添加到 main.jsp 中并尝试访问 * http://localhost:8080/main.jsp *。当你第一次运行时将会出现如下所示的结果：

<h2>Welcome to my website</h2>
<h3>Session Infomation</h3>
<table cellpadding="5" class="table table-bordered">
<tr bgcolor="#949494">
  <th>Session info</th><th>value</th></tr>
<tr>
  <td>id</td>
  <td>0AE3EC93FF44E3C525B4351B77ABB2D5</td></tr>
<tr>
  <td>Creation Time</td>
  <td>Tue Jun 08 17:26:40 GMT+04:00 2010  </td></tr>
<tr>
  <td>Time of Last Access</td>
  <td>Tue Jun 08 17:26:40 GMT+04:00 2010  </td></tr>
<tr>
  <td>User ID</td>
  <td>ABCD  </td></tr>
<tr>
  <td>Number of visits</td>
  <td>0</td></tr>
</table>  

现在尝试第二次运行相同的 JSP，将会出现如下所示的结果。

<h2>Welcome Back to my website</h2>
<h3>Session Infomation</h3>
<table cellpadding="5" class="table table-bordered">
<tr bgcolor="#949494">
  <th>info type</th><th>value</th></tr>
<tr>
  <td>id</td>
  <td>0AE3EC93FF44E3C525B4351B77ABB2D5</td></tr>
<tr>
  <td>Creation Time</td>
  <td>Tue Jun 08 17:26:40 GMT+04:00 2010  </td></tr>
<tr>
  <td>Time of Last Access</td>
  <td>Tue Jun 08 17:26:40 GMT+04:00 2010  </td></tr>
<tr>
  <td>User ID</td>
  <td>ABCD  </td></tr>
<tr>
  <td>Number of visits</td>
  <td>1</td></tr>
</table>  

## 删除会话数据：

当你完成了用户会话数据，你有以下几种选择：

- **删除一个特定的属性：** 你可以调用 * public void removeAttribute(String name) * 方法来删除与特定的键相关的值。

- **删除整个会话：** 你可以调用 * public void invalidate() * 方法来删除整个会话。

- **设置会话超时：** 你可以调用 * public void setMaxInactiveInterval(int interval) * 方法分别为每个会话设置超时。

- **注销用户：** 服务器可以支持 servlet  2.4，你可以调用 **logout** 来注销 Web 服务器的客户端，并使所有属于该的用户的会话无效。

- **web.xml 配置：** 如果你使用的是 Tomcat，除了上述方法外，你还可以在 web.xml文件中设置会话超时，如下所示。

``` 
<session-config>
    <session-timeout>15</session-timeout>
  </session-config>
```

超时以分钟为单位，在 Tomcat 中，默认的超时为 30 分钟。

在 servlet 中的 getMaxInactiveInterval() 方法为会话一个以秒为单位的超时时间。所以如果你的会话在 web.xml 中设置为 15 分钟，那么 getMaxInactiveInterval() 返回 900。
