# JSP 调试 

测试或者调试一个 JSP 和 servlets 总是很困难的。JSP 和 servlets 往往涉及到大量的客户端/服务器之间的交互，可能会出现错误并且很难再生成。 

这里有一些提示和建议，可能会在你的调试中帮助你。 

## 使用 System.out.println()： 

System.out.println() 在测试中作为一个标记很容易使用，不管某段代码是否被执行。我们也可以输出变量值。另外：

- 由于系统对象是 Java 对象核心的一部分，它可以在任何地方被使用而不需要安装额外的类。这包括 Servlets， JSP， RMI， EJB's， ordinary Beans 和 classes， 和独立的应用程序。

- 与停在断点相比较，写到 System.out 中并没有对应用程序正常的执行流产生过多的干扰，当时间至关重要时，这使得它非常有价值。

下面是使用 System.out.println() 的语法：

```
System.out.println("Debugging message");
```

下面是使用 System.out.println() 的一个简单的例子：

```
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head><title>System.out.println</title></head>
<body>
<c:forEach var="counter" begin="1" end="10" step="1" >
   <c:out value="${counter-5}"/></br>
   <% System.out.println( "counter= " + 
                     pageContext.findAttribute("counter") ); %>
</c:forEach>
</body>
</html>
```

现在如果你要试图访问上面的 JSP，它将会在浏览器上产生以下的结果：

```
-4
-3
-2
-1
0
1
2
3
4
5
```


如果你使用的是 Tomcat，你还将发现这些行会被附加到日志目录里 stdout.log  文件的末尾。

```
counter=1
counter=2
counter=3
counter=4
counter=5
counter=6
counter=7
counter=8
counter=9
counter=10
```


这样你可以把变量和其他信息打印到系统日志中，可以分析找到问题的根本原因或者其他各种原因。 

## 使用 JDB 记录器： 

J2SE 日志框架旨在为 JVM 中运行的任何类提供日志服务。所以我们可以利用这个框架来记录任何信息。

让我们使用 JDK 记录器 API 重写上面的示例：

```
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@page import="java.util.logging.Logger" %>

<html>
<head><title>Logger.info</title></head>
<body>
<% Logger logger=Logger.getLogger(this.getClass().getName());%>

<c:forEach var="counter" begin="1" end="10" step="1" >
   <c:set var="myCount" value="${counter-5}" />
   <c:out value="${myCount}"/></br>
   <% String message = "counter="
                  + pageContext.findAttribute("counter")
                  + " myCount="
                  + pageContext.findAttribute("myCount");
                  logger.info( message );
   %>
</c:forEach>
</body>
</html>
```

这将在浏览器和 stdout.log 中生成相似的结果，但是会在 stdout.log 文件中有附加信息。在这里，我们使用记录器的 **info** 方法，因为我们只是为了信息的目的在记录消息。这是 stdout.log 文件的一个快照：

```
24-Sep-2010 23:31:31 org.apache.jsp.main_jsp _jspService
INFO: counter=1 myCount=-4
24-Sep-2010 23:31:31 org.apache.jsp.main_jsp _jspService
INFO: counter=2 myCount=-3
24-Sep-2010 23:31:31 org.apache.jsp.main_jsp _jspService
INFO: counter=3 myCount=-2
24-Sep-2010 23:31:31 org.apache.jsp.main_jsp _jspService
INFO: counter=4 myCount=-1
24-Sep-2010 23:31:31 org.apache.jsp.main_jsp _jspService
INFO: counter=5 myCount=0
24-Sep-2010 23:31:31 org.apache.jsp.main_jsp _jspService
INFO: counter=6 myCount=1
24-Sep-2010 23:31:31 org.apache.jsp.main_jsp _jspService
INFO: counter=7 myCount=2
24-Sep-2010 23:31:31 org.apache.jsp.main_jsp _jspService
INFO: counter=8 myCount=3
24-Sep-2010 23:31:31 org.apache.jsp.main_jsp _jspService
INFO: counter=9 myCount=4
24-Sep-2010 23:31:31 org.apache.jsp.main_jsp _jspService
INFO: counter=10 myCount=5
```


可以通过使用方便的函数发送各种级别的消息，如 severe()， warning()， info()， config()， fine()， finer()， 和  finest()。这里，finest()  方法可以用于记录最好的信息，severe()  方法可以用于记录严峻的消息。

你可以使用 [Log4J Framework](http://www.tutorialspoint.com/log4j/index.htm) 在不同的文件中根据消息的严重水平和重要性来记录他们。 

## 调试工具： 

NetBeans 是一个免费和开源的 Java 集成开发环境，支持独立的 Java 应用程序和 web 应用程序的开发，支持 JSP 和 servlet 规范，也包括一个 JSP 调试器。 

NetBeans 支持以下基本的调试功能： 

- 断点

- 单步调试

- 监视点

你可以参考 NetBeans 文档来了解上面的调试功能。

## 使用 JDB 调试器：

你可以使用与你用来调试小程序和应用程序相同的 **jdb** 命令来调试 JSP 和 servlets 。

为了调试 JSP 和 servlets，你可以调试 sun.servlet.http.HttpServer，然后在来自浏览器的 HTTP 请求的响应里查看 HttpServer 正在执行的 JSP/servlets。这和如何调试小程序非常相似。不同不处是，在小程序里，真正的程序是在 sun.applet.AppletViewer 里调试的。 

大多数调试器通过自动得知如何调试小程序来隐藏这些细节。直到它们对 JSP 做着同样的操作，你必须帮助你的调试器执行以下操作： 

- 设置你的调试器的类路径，以便于找到 sun.servlet.Http-Server 和与其相关的类。

- 设置你的调试器的类路径，以便于找到你的 JSP 和支持的类，典型的是 ROOT\WEB-INF\classes。

一旦你已经正确的设置了类路径，开始调试 sun.servlet.http.HttpServer。对于一个给定的 JSP，你可以在你感兴趣的任何地方设置断点，然后通过一个 web 浏览器来发送一个请求到 HttpServer (http://localhost:8080/JSPToDebug )。你会看到执行会在你设置的断点处停止。

## 使用注释：

你代码中的注释可以用不同的方法帮助你的调试过程。注释可以用于调试过程的很多其他方面。

JSP 使用 Java 命令和单线（//...）和多线（/*...*/）命令，可以暂时删除你 Java 代码的一部分。如果错误消失，仔细看看你的代码注释并找出问题所在。

## 客户端和服务器端头文件： 

有时，当一个 JSP 表现的不像预期的那样，查看一下原始的 HTTP 请求和响应是非常有用的。如果你熟悉 HTTP 的结构，你可以读取请求和响应，看看那些头文件中到底是社么信息。

## 重要的调试技巧： 

这里是一些关于 JSP 调试的调试技巧：

- 向浏览器查看它显示的页面的原始内容。这可以帮助识别格式问题。它通常是视图菜单下的一个选项。

- 确保浏览器不会通过强迫一个完全加载的页面来缓存先前的请求的输出。在 Netscape Navigator，使用 Shift-Reload；在 Internet Explorer ，使用 Shift-Refresh。
