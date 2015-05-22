# JSP - Cookies 处理

Cookies 是存储在客户端计算机的文本文件，保存各种跟踪目标的信息。JSP 使用底层 servlet 技术透明地支持 HTTP cookies。

确定返回用户有三个步骤：

- 服务器脚本向浏览器发送的一系列cookies。例如姓名、年龄、身份证号码等。

- 浏览器将这个信息存储在本地机器上，以供将来使用。

- 下次当浏览器向web服务器发送任何请求时，将这些 cookies 信息发送给服务器，服务器使用这些信息来识别用户或可能用于其他目的。

本章将教你如何设置或重置 cookies，如何访问它们，以及如何使用 JSP 程序删除它们。

## Cookie 的剖析

Cookie 通常设置在一个 HTTP 标题中(尽管 JavaScript 也可以在浏览器中直接设置cookie)。设置 cookie 的 JSP可能发送如下所示的标题信息：

``` 
HTTP/1.1 200 OK
Date: Fri, 04 Feb 2000 21:03:38 GMT
Server: Apache/1.3.9 (UNIX) PHP/4.0b3
Set-Cookie: name=xyz; expires=Friday, 04-Feb-07 22:03:38 GMT; 
                 path=/; domain=tutorialspoint.com
Connection: close
Content-Type: text/html
```

正如你所看见的，Set-Cookie 标题包含一个名称值对，GMT 时间，路径和一个域。名称和
值将被 URL 编码。结束字段是在给定的时间和日期之后，向浏览器发出指令来“忘记”cookie。

如果配置浏览器来存储 cookie，然后它会保存这个信息直到截止日期。如果用户在任何与cookie 的路径和域相匹配的页面点击浏览器，它将把 cookie 重新发送到服务器。浏览器的标题看起来如下所示：

``` 
GET / HTTP/1.0
Connection: Keep-Alive
User-Agent: Mozilla/4.6 (X11; I; Linux 2.2.6-15apmac ppc)
Host: zink.demon.co.uk:1126
Accept: image/gif, */*
Accept-Encoding: gzip
Accept-Language: en
Accept-Charset: iso-8859-1,*,utf-8
Cookie: name=xyz
```

## Servlet Cookies 方法

下面是与 Cookie 对象关联的有用的方法列表，你可以在 JSP 中操作 cookies 时使用：

<table class="table table-bordered">
<tr><th style="width:5%">S.N.</th><th>方法 &amp; 描述</th></tr>
<tr><td>1</td><td><p><b>public void setDomain(String pattern)</b></p>
<p>此方法设置了 cookie 适用的领域，例如 tutorialspoint.com。</p></td></tr>
<tr><td>2</td><td><p><b>public String getDomain()</b></p>
<p>此方法得到了 cookie 适用的领域，例如 tutorialspoint.com。</p></td></tr>
<tr><td>3</td><td><p><b>public void setMaxAge(int expiry)</b></p>
<p>该方法设置了在 cookie 到期之前需要多少时间(以秒为单位)。如果你不设置这个，cookie 只持续到当前会话。</p></td></tr>
<tr><td>4</td><td><p><b>public int getMaxAge()</b></p>
<p>该方法返回了最大持续时间的 cookie，以秒为单位指定，默认情况下，-1表示 cookie
会持续到浏览器关闭。</p></td></tr>
<tr><td>5</td><td><p><b>public String getName()</b></p>
<p>该方法将返回 cookie 的名称。这个名字创建后不能更改。</p></td></tr>
<tr><td>6</td><td><p><b>public void setValue(String newValue)</b></p>
<p>这个方法设置了与 cookie 相关的值。</p></td></tr>
<tr><td>7</td><td><p><b>public String getValue()</b></p>
<p>这个方法得到了与 cookie相关的值。</p></td></tr>
<tr><td>8</td><td><p><b>public void setPath(String uri)</b></p>
<p>该方法设置了 cookie 应用的路径。如果你不指定路径，那么与当前页面相同的目录以及子目录中的所有 URL都会返回 cookie。</p></td></tr>
<tr><td>9</td><td><p><b>public String getPath()</b></p>
<p>该方法获取 cookie 应用的路径。 </p></td></tr>
<tr><td>10</td><td><p><b>public void setSecure(boolean flag)</b></p>
<p>此方法设置布尔值，该值表明 cookie 是否只能通过加密连接发送(例如 SSL)。</p></td></tr>
<tr><td>11</td><td><p><b>public void setComment(String purpose)</b></p>
<p>这种方法指定了描述 cookie 目的的评论。如果浏览器向用户展示了这个 cookie，那么评论是有用的。</p></td></tr>
<tr><td>12</td><td><p><b>public String getComment()</b></p>
<p>该方法返回描述 cookie 目的的评论，如果 cookie 没有评论，那么返回 null。</p></td></tr>
</table>

## 用 JSP 设置 Cookies

用 JSP 设置 Cookies 包括三个步骤：

**(1) 创建一个 Cookie 对象：** 用 cookie 的名称和值调用 cookie 构造函数，名称和值是字符串。

``` 
Cookie cookie = new Cookie("key","value");
```

记住，这个名字和值都不应该包含空格或任何以下字符：

``` 
[ ] ( ) = , " / ? @ : ;
```

**(2) 设置最大持续时间：** 使用 setMaxAge 指定 cookie 的有效期是多长时间(以秒为单位)。以下是建立了一个持续 24 小时的 cookie。

``` 
cookie.setMaxAge(60*60*24); 
```

**(3) 将 cookie 发送到 HTTP 响应标题中：** 使用 **response.addCookie** 在 HTTP 响应标题中添加 cookies，如下所示：

``` 
response.addCookie(cookie);
```

## 示例：

让我们修改 [表单示例](form-processing.md) 为名称设置 cookies。

<pre class="prettyprint notranslate">
&lt;%
   // Create cookies for first and last names.      
   Cookie firstName = new Cookie("first_name",
 			  request.getParameter("first_name"));
   Cookie lastName = new Cookie("last_name",
			  request.getParameter("last_name"));

   // Set expiry date after 24 Hrs for both the cookies.
   firstName.setMaxAge(60*60*24); 
   lastName.setMaxAge(60*60*24); 

   // Add both the cookies in the response header.
   response.addCookie( firstName );
   response.addCookie( lastName );
%&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Setting Cookies&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;Setting Cookies&lt;/h1&gt;
&lt;/center&gt;
&lt;ul&gt;
&lt;li&gt;&lt;p&gt;&lt;b&gt;First Name:&lt;/b&gt;
   &lt;%= request.getParameter("first_name")%&gt;
&lt;/p&gt;&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;b&gt;Last  Name:&lt;/b&gt;
   &lt;%= request.getParameter("last_name")%&gt;
&lt;/p&gt;&lt;/li&gt;
&lt;/ul&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


将上述代码添加到 main.jsp 文件中，并在下述的 HTML 页面中使用：

<pre class="prettyprint notranslate"> 
&lt;html&gt;
&lt;body&gt;
&lt;form action="main.jsp" method="GET"&gt;
First Name: &lt;input type="text" name="first_name"&gt;
&lt;br /&gt;
Last Name: &lt;input type="text" name="last_name" /&gt;
&lt;input type="submit" value="Submit" /&gt;
&lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>



将上述 HTML 内容保存在hello.jsp 文件中，并将hello.jsp 和 main.jsp 添加到 < Tomcat-installation-directory > / webapps /ROOT 目录中。当你访问 http:// localhost:8080/hello.jsp时，这是表单上的实际输出。

<form action="javascript:void();" method="get" target="_blank"> 
First Name: <input type="text" name="first_name" />  <br /> 
 
Last Name: <input type="text" name="last_name" /> 
<input type="button" value="Submit" /> 
</form>

尝试输入姓名，然后单击 submit 按钮。这将在你的屏幕上显示姓名，同时会设置 firstName
和 lastName 这两个 cookie，当你下次点击 submit 按钮时，将传回服务器。

下一节将解释如何在你的web应用程序中访问这些 cookies。

## 用 JSP 读取 Cookies

想要读取 cookie，你需要通过调用 HttpServletRequest 的 getCookies() 方法创建一个 *javax.servlet.http* 数组。然后通过数组循环，使用 getName() 和 getValue() 方法来访问每个 cookie 和相关的值。

## 示例

让我们读取之前例子中设置的 cookies：

<pre class="prettyprint notranslate tryit">
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Reading Cookies&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;Reading Cookies&lt;/h1&gt;
&lt;/center&gt;
&lt;%
   Cookie cookie = null;
   Cookie[] cookies = null;
   // Get an array of Cookies associated with this domain
   cookies = request.getCookies();
   if( cookies != null ){
      out.println("&lt;h2&gt; Found Cookies Name and Value&lt;/h2&gt;");
      for (int i = 0; i &lt; cookies.length; i++){
         cookie = cookies[i];
         out.print("Name : " + cookie.getName( ) + ",  ");
         out.print("Value: " + cookie.getValue( )+" &lt;br/&gt;");
      }
  }else{
      out.println("&lt;h2&gt;No cookies founds&lt;/h2&gt;");
  }
%&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在让我们将上面的代码放在 main.jsp 文件中并试图访问它。如果你要设置 first_name cookie为“John”，last_name cookie 为“Player”，然后运行 http:// localhost:8080/main.jsp，将显示下面的结果：

<pre class="result notranslate">
<h2> Found Cookies Name and Value</h2>
<p>Name : first_name, Value: John </p>
<p>Name : last_name,  Value: Player</p>
</pre>



## 用 JSP 删除 Cookies

删除 cookies 非常简单。如果你想删除一个 cookie，那么你只需要按照以下三步来处理：

- 读取一个已经存在的 cookie 并把它保存在 Cookie 对象中。

- 使用 **setMaxAge()** 方法将 cookie 的持续时间设置为 0 来删除一个已经存在的 cookie。

- 将这个 cookie 添加到响应标题中。

## 示例

以下的例子中删除了现存的命名为“first_name”的 cookie，当你下次运行 main.jsp JSP时，first_name 会返回空值。

<pre class="prettyprint notranslate tryit">
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Reading Cookies&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;Reading Cookies&lt;/h1&gt;
&lt;/center&gt;
&lt;%
   Cookie cookie = null;
   Cookie[] cookies = null;
   // Get an array of Cookies associated with this domain
   cookies = request.getCookies();
   if( cookies != null ){
      out.println("&lt;h2&gt; Found Cookies Name and Value&lt;/h2&gt;");
      for (int i = 0; i &lt; cookies.length; i++){
         cookie = cookies[i];
         if((cookie.getName( )).compareTo("first_name") == 0 ){
            cookie.setMaxAge(0);
            response.addCookie(cookie);
            out.print("Deleted cookie: " + 
            cookie.getName( ) + "&lt;br/&gt;");
         }
         out.print("Name : " + cookie.getName( ) + ",  ");
         out.print("Value: " + cookie.getValue( )+" &lt;br/&gt;");
      }
  }else{
      out.println(
      "&lt;h2&gt;No cookies founds&lt;/h2&gt;");
  }
%&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在将上述代码添加到 main.jsp 中并尝试访问它。它会出现如下所示的结果：

<pre class="result notranslate">
<h2>Cookies Name and Value</h2>
<p>Deleted cookie : first_name</p>
<p>Name : first_name, Value: John</p>
<p>Name : last_name,  Value: Player</p>
</pre>


现在尝试再次运行 *http://localhost:8080/main.jsp*，只会出现如下所示的一个 cookie：

<pre class="result notranslate">
<h2> Found Cookies Name and Value</h2>
Name : last_name,  Value: Player
</pre>


你可以在 IE 浏览器中自动的删除你的 cookies。单击工具菜单并选择网络选项。要删除所有 cookie，按下 Delete Cookies。
