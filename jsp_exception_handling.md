# JSP - 异常处理 

当你写 JSP 代码的时候，程序员有可能会留下一个编码错误，并且它会出现在代码的任何一个部分。在你的 JSP 代码中你会有以下类型的错误： 

- **检测异常：** 一个检测异常通常是一个用户错误或者是一个有程序员无法预见的错误引起的异常。例如，如果要打开一个文件，但是无法找到该文件，这时就会出现异常。这些异常在编译时不能简单的忽略掉。

- **运行异常：** 一个运行异常可能是程序员本来可以避免的一个异常。和检测异常相反，运行异常在编译时可以被忽略。

- **错误：** 这原本不是异常，是超出用户或者程序员的控制而引起的问题。错误通常在你的代码中会被忽略，因为你对一个错误能够做的很少。例如，如果一个堆栈发生溢出，那么就会出现一个错误。在编译时他们也会被忽略。

本教程将会对你的 JSP 代码，给你一些简单而又优雅的处理运行异常和错误的方法。

## 使用异常对象

异常对象是 Throwable 子类的一个实例（例如，java.lang.NullPointerException），它只能在错误页面是可用的。下面是 Throwable 类中可用的重要方法的列表。 

<table class="table table-bordered"> 
	<tr> 
	<th style="width:5%">序号</th><th style="width:95%">方法及描述</th></tr> 
	<tr><td>1</td><td><b>public String getMessage()</b></p> 
	<p>返回发生异常的详细信息。这个消息是在 Throwable 构造函数里初始化的。
	</p></td></tr> 
	<tr><td>2</td><td><b>public Throwable getCause()</b></p> 
	<p>返回发生异常的原因，用一个 Throwable 对象表示。</p></td></tr> 
	<tr><td>3</td><td><b>public String toString()</b></p> 
	<p>返回与 getMessage() 相连接的类名。</p></td></tr> 
	<tr><td>4</td><td><b>public void printStackTrace()</b></p> 
	<p>输出 toString() 和堆栈跟踪的 System.err 的结果，错误输出流。</p></td></tr> 
	<tr><td>5</td><td><b>public StackTraceElement [] getStackTrace()</b></p> 
	<p>返回一个数组，其中包含堆栈跟踪的每一个元素。索引值为0的元素表示调用堆栈的顶部，
	数组中最后一个元素在调用堆栈的底部代表方法。</p></td></tr> 
	<tr><td>6</td><td><b>public Throwable fillInStackTrace()</b></p> 
	<p>用当前的堆栈跟踪填满 Throwable 对象的堆栈跟踪，添加任何先前的堆栈跟踪信息。</p></td></tr> 
	</table> 

JSP 会给你一个选项来指定每一个 JSP 的错误页面。不管何时页面抛出一个异常，JSP 容器都会自动的调用错误页面。

下面是 main.jsp 中一个特定错误页面的例子。为了创建一个错误页面，使用 <%@ page errorPage=”xxx”%> 指令。

```
<%@ page errorPage="ShowError.jsp" %>

<html>
<head>
   <title>Error Handling Example</title>
</head>
<body>
<%
   // Throw an exception to invoke the error page
   int x = 1;
   if (x == 1)
   {
      throw new RuntimeException("Error condition!!!");
   }
%>
</body>
</html>
```

现在你需要写一个错误处理的 JSP ShowError.jsp，下面给出了代码。注意，错误处理页面包括 <%@ page isErrorPage=”true”%> 指令。这个指令使 JSP 编译器生成异常实例变量。

```
<%@ page isErrorPage="true" %>
<html>
<head>
<title>Show Error Page</title>
</head>
<body>
<h1>Opps...</h1>
<p>Sorry, an error occurred.</p>
<p>Here is the exception stack trace: </p>
<pre>
<% exception.printStackTrace(response.getWriter()); %>
</pre>
</body>
</html>
```

现在试图访问 main.jsp，它将会生成如下结果：

```
java.lang.RuntimeException: Error condition!!!
......

Opps...
Sorry, an error occurred.

Here is the exception stack trace:
```

## 在错误页面使用 JSTL 标签

你可以使用 JSTL 标签来编写一个错误页面 ShowError.jsp。这个页面和上面的例子中几乎使用的是相同的逻辑，但是它有更好的结构，并且他提供了更多的信息：

```
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@page isErrorPage="true" %>
<html>
<head>
<title>Show Error Page</title>
</head>
<body>
<h1>Opps...</h1>
<table width="100%" border="1">
<tr valign="top">
<td width="40%"><b>Error:</b></td>
<td>${pageContext.exception}</td>
</tr>
<tr valign="top">
<td><b>URI:</b></td>
<td>${pageContext.errorData.requestURI}</td>
</tr>
<tr valign="top">
<td><b>Status code:</b></td>
<td>${pageContext.errorData.statusCode}</td>
</tr>
<tr valign="top">
<td><b>Stack trace:</b></td>
<td>
<c:forEach var="trace" 
         items="${pageContext.exception.stackTrace}">
<p>${trace}</p>
</c:forEach>
</td>
</tr>
</table>
</body>
</html>
```

现在试图访问 main.jsp，它将会生成如下结果：

<pre class="result notranslate">
<h1>Opps...</h1>
<table width="100%" border="1">
<tr valign="top">
<td width="40%"><b>Error:</b></td>
<td>java.lang.RuntimeException: Error condition!!!</td>
</tr>
<tr valign="top">
<td><b>URI:</b></td>
<td>/main.jsp</td>
</tr>
<tr valign="top">
<td><b>Status code:</b></td>
<td>500</td>
</tr>
<tr valign="top">
<td><b>Stack trace:</b></td>
<td>
<p>org.apache.jsp.main_jsp._jspService(main_jsp.java:65)</p>
<p>org.apache.jasper.runtime.HttpJspBase.service(HttpJspBase.java:68)</p>
<p>javax.servlet.http.HttpServlet.service(HttpServlet.java:722)</p>
<p>org.apache.jasper.servlet.JspServlet.service(JspServlet.java:265)</p>
<p>javax.servlet.http.HttpServlet.service(HttpServlet.java:722)</p>
................... 
</td>
</tr>
</table>
</pre>

## 使用 Try...Catch 块

如果你想要在同一个页面中处理错误，使用一些动作而不是释放一个错误页面，那么你可以利用 Try...catch 块。

下面显示的是如何使用 try...catch 块的一个简单的例子。让我们将下面发的代码放到 main.jsp 中：

```
<html>
<head>
   <title>Try...Catch Example</title>
</head>
<body>
<%
   try{
      int i = 1;
      i = i / 0;
      out.println("The answer is " + i);
   }
   catch (Exception e){
      out.println("An exception occurred: " + e.getMessage());
   }
%>
</body>
</html>
```

现在试图访问 main.jsp，它将会生成如下结果：

```
An exception occurred: / by zero 
```