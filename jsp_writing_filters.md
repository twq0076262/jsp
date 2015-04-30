# JSP——过滤器

Servlet 和 JSP 过滤器都是 Java 类，可以在 Servlet 和 JSP 编程中用于以下目的：

- 在请求访问后端资源之前从客户端拦截请求。

- 在响应发送回客户端之前从服务器操作响应。

有各种符合规格的过滤器：

- 身份验证过滤器。

- 数据压缩过滤器

- 加密过滤器。

- 触发资源访问事件的过滤器。

- 图像转换过滤器。

- 日志记录和审计过滤器。

- MIME 类型链过滤器。

- Tokenizing 过滤器。

- 转换 XML 内容的 XSL/T 过滤器。

过滤器是部署在部署描述符文件 **web.xml** 中的，然后映射到应用程序的部署描述符中
的 servlet 或 JSP 名称或URL 模式。部署描述符文件 web.xml 可以在 *< 
Tomcat-installation-directory > \ conf* 目录下找到。

当 JSP 容器启动 web 应用程序时，它会为每个在部署描述符中声明的过滤器创建一个实例。过滤器按照它们在部署描述符中声明的顺序执行。

## Servlet 过滤器方法：

一个过滤器是一个简单的 Java 类，实现了 javax.servlet.Filter 接口。javax.servlet.Filter接口定义了三个方法：

<table class="table table-bordered">
<tr><th style="width:5%">S.N.</th><th>方法 &amp; 描述</th></tr>
<tr><td>1</td><td><p><b>public void doFilter (ServletRequest, ServletResponse, FilterChain)</b></p>
<p>由于客户端在链尾请求响应，每次请求/响应对通过链时，容器会调用此方法。</p></td></tr>
<tr><td>2</td><td><p><b>public void init(FilterConfig filterConfig)</b></p>
<p>由 web 容器调用此方法，向过滤器表明它将被放置在服务中。</p></td></tr>
<tr><td>3</td><td><p><b>public void destroy()</b></p>
<p>由 web 容器调用此方法，向过滤器表明它将从服务中被去掉。</p></td></tr>
</table> 
## JSP 过滤器示例：

下面是 JSP 过滤器的示例，每次访问任何 JSP 文件时都会输出客户端 IP 地址和当前日期时间。这个例子会使你基本了解 JSP 过滤器，但是你可以使用相同的概念编写更复杂的过滤器应用程序：

<pre class="prettyprint notranslate">
// Import required java libraries
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.util.*;
 
// Implements Filter class
public class LogFilter implements Filter  {
   public void  init(FilterConfig config) 
                         throws ServletException{
      // Get init parameter 
      String testParam = config.getInitParameter("test-param"); 
 
      //Print the init parameter 
      System.out.println("Test Param: " + testParam); 
   }
   public void  doFilter(ServletRequest request, 
                 ServletResponse response,
                 FilterChain chain) 
                 throws java.io.IOException, ServletException {
 
      // Get the IP address of client machine.   
      String ipAddress = request.getRemoteAddr();
 
      // Log the IP address and current timestamp.
      System.out.println("IP "+ ipAddress + ", Time "
                                       + new Date().toString());
 
      // Pass request back down the filter chain
      chain.doFilter(request,response);
   }
   public void destroy( ){
      /* Called before the Filter instance is removed 
      from service by the web container*/
   }
}
</pre>


以通常的方式编译 **LogFilter.java**，把 LogFilter.class 类文件放在 < Tomcat-installation-directory > / webapps /ROOT/ web - inf / classes 中。

## 在 Web.xml 中的 JSP 过滤器映射

首先定义过滤器，然后将过滤器映射到 URL 或 JSP 文件的名字中，这几乎与定义 Servlet
然后映射到 web. Xml 文件的 URL 模式的方式相同。为在部署描述符文件 **web.xml**
的过滤器标签创建以下条目

``` 
<filter>
   <filter-name>LogFilter</filter-name>
   <filter-class>LogFilter</filter-class>
   <init-param>
	  <param-name>test-param</param-name>
	  <param-value>Initialization Paramter</param-value>
   </init-param>
</filter>
<filter-mapping>
   <filter-name>LogFilter</filter-name>
   <url-pattern>/*</url-pattern>
</filter-mapping>
```

上面的过滤器将适用于所有 servlet 和 JSP，因为我们在配置中指定了**/ ***。如果你想把
过滤器应用到部分 servlet 或 JSP 中，你可以指定一个特定的 servlet 或 JSP 路径。

现在尝试以常用的方式调用任何 servlet 或 JSP，你会在 web 服务器日志中看到生成的登
录。你可以使用 Log4J 日志在一个单独的文件中记录上面的登录。

## 使用多个过滤器

你的 web 应用程序可能定义了带有特定目的的不同的过滤器。考虑这个情况，你定义两个过滤器 *AuthenFilter* 和 *LogFilter*。剩下的过程仍将像前面解释的那样，除了你需要创建一个不同的映射，如下所示：

``` 
<filter>
   <filter-name>LogFilter</filter-name>
   <filter-class>LogFilter</filter-class>
   <init-param>
	  <param-name>test-param</param-name>
	  <param-value>Initialization Paramter</param-value>
   </init-param>
</filter>
<filter>
   <filter-name>AuthenFilter</filter-name>
   <filter-class>AuthenFilter</filter-class>
   <init-param>
	  <param-name>test-param</param-name>
	  <param-value>Initialization Paramter</param-value>
   </init-param>
</filter>
<filter-mapping>
   <filter-name>LogFilter</filter-name>
   <url-pattern>/*</url-pattern>
</filter-mapping>
<filter-mapping>
   <filter-name>AuthenFilter</filter-name>
   <url-pattern>/*</url-pattern>
</filter-mapping>
```

## 过滤器的应用顺序

在 web.xml 中的 filter-mapping 元素的顺序决定了 web 容器把过滤器应用到 servlet 或JSP 的顺序。想要逆转滤波器的顺序，你只需要逆转 web.xml 文件中的 filter-mapping 元素。

例如，上面的例子将首先应用 LogFilter ，然后应用 AuthenFilter 到任意 servlet 或 JSP 中，但是下面的例子将逆转这个顺序：

``` 
<filter-mapping>
   <filter-name>AuthenFilter</filter-name>
   <url-pattern>/*</url-pattern>
</filter-mapping>
<filter-mapping>
   <filter-name>LogFilter</filter-name>
   <url-pattern>/*</url-pattern>
</filter-mapping>
```


