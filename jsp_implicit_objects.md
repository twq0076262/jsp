# JSP——隐式对象

JSP 隐式对象是 Java 对象，JSP 容器使隐式对象在每一个页面中对开发人员是可用的，开发人员可以直接调用它们而不用显式声明。JSP 隐式对象也称为预定义的变量。

JSP 支持九个隐式对象，如下所示：

<table class="table table-bordered">
<tr><th style="width:30%">对象</th><th>描述</th></tr>
<tr><td>request</td><td>这是与请求关联的 <b>HttpServletRequest</b> 对象。</td></tr>
<tr><td>response</td><td>这是与客户端响应关联的 <b>HttpServletResponse</b> 对象。</td></tr>
<tr><td>out</td><td>这是用于向客户端发送输出的 <b>PrintWriter</b> 对象。</td></tr>
<tr><td>session</td><td>这是与请求关联的 <b>HttpSession</b> 对象。</td></tr>
<tr><td>application</td><td>这是与应用程序上下文关联的 <b>ServletContext</b> 对象。</td></tr>
<tr><td>config</td><td>这是与页面关联的 <b>servletConfig</b> 对象。</td></tr>
<tr><td>pageContext</td><td>这个封装特使用特定服务器的特性，如更高的性能 <b>jspwriter</b>。</td></tr>
<tr><td>page</td><td>这是 <b>this</b> 的一个简单的同义词，是用来调用由转换的 servlet 类定义的方法。</td></tr>
<tr><td>Exception</td><td> <b>Exception</b> 对象允许指定的 JSP 访问异常数据。</td></tr>
</table>

## request 对象：

request 对象是 javax.servlet.http.HttpServletRequest 对象的一个实例。每次客户端请求一个页面时，JSP 引擎都会创建一个新的对象来表示那个请求。

Request 对象提供方法来获取 HTTP 头信息，包括表单数据，cookies，HTTP 方法等。

我们将会在接下来的章节中看到与 request 对象相关的完整的方法集合：[**JSP - Client Request**](http://www.tutorialspoint.com/jsp/jsp_client_request.htm)

## response 对象：

Response 对象是 javax.servlet.http.HttpServletResponse 对象的一个实例。当服务器创建 request 对象时，它也创建了代表客户端响应的对象。

Response 对象还定义了接口，可以处理创建的新的 HTTP 头。通过这个对象 JSP 程序员可以添加新的 cookies 或日期 stamps，HTTP 状态码等。

我们将会在接下来的章节中看到与 response 对象相关的完整的方法集合：[**JSP - Server Response**](http://www.tutorialspoint.com/jsp/jsp_server_response.htm)

## out 对象

out 隐式对象是 javax.servlet.jsp. JspWriter 对象的一个实例，用于在响应中发送内容。

最初的 JspWriter 对象被实例化不同程度地取决于页面是否缓冲。通过使用页面指令的 buffered='false' 属性，缓冲可以很容易地关掉。

JspWriter 对象包含大部分与 java.io.PrintWriter 类相同的方法。然而，JspWriter 对象有一些额外的方法用来处理缓冲。与 PrintWriter 对象不同，JspWriter 抛出 IOException。

以下是我们用来写布尔型 char，int，double，object，String 等等的重要方法。

<table class="table table-bordered">
<tr><th style="width:40%">方法</th><th> 描述 </th></tr>
<tr><td><b>out.print(dataType dt)</b></td><td>输出一个数据类型的值</td></tr>
<tr><td><b>out.println(dataType dt)</b></td><td>输出数据类型值然后用新行字符终止该行。</td></tr>
<tr><td><b>out.flush()</b></td><td> 刷新数据流。</td></tr>
</table>  

## session 对象：

Session 对象是 javax.servlet.http.HttpSession 的一个实例，且行为与 Java servlet 中的 session 对象完全相同。

Session 对象是用来跟踪客户端请求之间的客户端会话。我们将在后续的章节中看到完整的使用 session 对象的方法：[**JSP - Session Tracking**](http://www.tutorialspoint.com/jsp/jsp_session_tracking.htm)

## application 对象

Application 对象是用于生成的 Servlet 的 ServletContext 对象的直接包装器，且实际上是 javax.servlet.ServletContext 对象的一个实例。

这个对象是 JSP 页面整个生命周期的一个代表。当初始化 JSP 页面时，这个对象被创建，当 JSP 页面由 jspDestroy()方法删除时，该对象也会被删除。

通过为 application 添加属性，你可以确保生成 web 应用程序的所有 JSP 文件可以访问它。

你可以在 [**JSP - Hits Counter**](http://www.tutorialspoint.com/jsp/jsp_hits_counter.htm) 章节中查看简单的使用 Application 对象的例子。

## Config 对象

Config 对象是 javax.servlet.ServletConfig 的一个实例，且是用于生成的 servlet 的 ServletConfig 对象的直接包装器。

该对象允许 JSP 程序员访问 Servlet 或 JSP 引擎初始化参数，如路径或文件位置等。

下面的 config 方法是唯一一个你可能曾经使用的方法，且它的使用很简单：

``` 
config.getServletName();
```

这返回 servlet 的名称，该名称是包含在定义在 web - inf \ web.xml 文件中< servlet-name >元素中的字符串。

## pageContext 对象：

PageContext 对象是 javax.servlet.jsp.PageContext 对象的一个实例。pageContext 对象用于表示整个 JSP 页面。

这个对象是作为一种手段来访问页面信息的,同时避免了大部分的实现细节。

这个对象为每个请求存储了请求引用和响应对象。Application，config，session，out 对象是通过访问该对象的属性派生出来的。

pageContext 对象还包含发布到 JSP 页面的指令信息，包括缓冲信息，errorPageURL，页面范围。

PageContext 类定义了几个领域，包括 PAGE_SCOPE ，REQUEST_SCOPE，SESSION_SCOPE，和APPLICATION_SCOPE，它确定了这四个范围。它还支持 40 多个方法，大约一半的方法是继承了 javax.servlet.jsp.JspContext 类的。

重要方法之一是 **removeAttribute**，该方法接受一个或两个参数。例如，pageContext.removeAttribute(“attrName”) 从全部范围中删除属性，而下面的代码仅从页面范围中删除它：

``` 
pageContext.removeAttribute("attrName", PAGE_SCOPE);
```

你可以在后续的章节中查看使用 pageContext 的例子：[**JSP - File Uploading**](http://www.tutorialspoint.com/jsp/jsp_file_uploading.htm)。

## Page 对象：

这个对象是一个页面实例的真实引用。它可以被认为是一个对象，代表了整个 JSP 页面。

Page 对象实际上是 **this** 对象的一个直接的同义词。

## exception 对象：

Exception 对象是一个包装器，包含来自先前页面的异常抛出。它通常用于为错误条件生成一个适当的响应。

我们将在后续章节中看到完整的使用该对象的例子：[**JSP - Exception Handling**](http://www.tutorialspoint.com/jsp/jsp_exception_handling.htm)。
