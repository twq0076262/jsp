# 页面重定向 

页面重定向通常用于当一个文件移动到一个新的位置，我们需要向客户端发送到这个新
的位置，或可能是因为负载平衡，或简单随机化。 

请求重定向到另一个页面的最简单的方法是使用 response 对象的 **sendRedirect()** 方法。以下是该方法的符号描述： 

``` 
public void response.sendRedirect(String location)
throws IOException 
```

此方法返回带有状态编码和新的页面位置的响应给浏览器。你也可以一起使用 setstatus() 和 setheader() 方法实现相同的重定向。

``` 
....
String site = "http://www.newpage.com" ;
response.setStatus(response.SC_MOVED_TEMPORARILY);
response.setHeader("Location", site); 
....
```

## 例子： 

这个例子显示了如何将一个 JSP 页面重定向到另一个位置：

<pre class="prettyprint notranslate">
&lt;%@ page import="java.io.*,java.util.*" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Page Redirection&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;Page Redirection&lt;/h1&gt;
&lt;/center&gt;
&lt;%
   // New location to be redirected
   String site = new String("http://www.photofuntoos.com");
   response.setStatus(response.SC_MOVED_TEMPORARILY);
   response.setHeader("Location", site); 
%&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在将上面的代码放在 PageRedirect.jsp 中，并且使用 URL http://localhost:8080/PageRedirect.jsp 来调用此 JSP。它将跳转到页面 http://www.photofuntoos.com。

