# JSP——概述

## 什么是 Java 服务器页面?

Java 服务器页面(JSP)是一种技术，能够开发支持动态内容的网页，可以帮助开发人员在 HTML 页面中利用特殊的 JSP 标签插入 java 代码，其中大部分标签是以<% 开始，以 %>结束的。

JavaServer Pages 组件是 Java servlet 的一种，旨在为 Java web 应用程序实现一个用户界面。Web 开发人员编写 JSP 作为文本文件，结合 HTML 或 XHTML 代码，XML 元素，并嵌入 JSP 操作和命令。

使用 JSP，你可以通过 web 页面的形式收集来自用户的输入，来自数据库或其他资源的当前记录并动态地创建 web 页面。

JSP 标签可用于各种用途，如从数据库检索信息或注册用户首选项，访问 javabean 组件，在页面之间传递控制，在请求、页面之间共享信息等。

## 为什么使用 JSP？

JavaServer Pages 的服务通常与通用网关接口(CGI)实现程序一样。但 JSP 与 CGI 相比，有几个优势。

- 性能更好，因为 JSP 允许在 HTML 页面本身嵌入动态元素而不需要创建一个单独的 CGI 文件。

- JSP 总是在服务器处理之前进行编译，不像 CGI/Perl，每次请求页面时都需要服务器加载一个解释器和目标脚本。

- JavaServer Pages 是建立在 Java servlet API 之上的，就像 servlet，JSP 也可以访问所有强大的 Enterprise Java API，包括 JDBC，JNDI，EJB，JAXP 等等。

- JSP 页面可以与 servlet 结合使用，来处理业务逻辑，该模型是由 Java servlet 模板引擎支持的。

最后，JSP 还是 Java EE 不可分割的一部分，是 enterprise 级别应用程序的一个完整平台。这意味着 JSP 可以用于从最简单的应用程序到最复杂的应用程序中，并实现要求。

## JSP 的优点

下列是 JSP 优于其他技术的另外的优点：

- **与 Active Server Pages(ASP)相比：** JSP 的优点是双重的。首先，动态的部分是用 Java 编写的，而不是用 Visual Basic 或其他特定的语言编写，所以它使用起来更强大并且更容易。第二，它可以移植到其他操作系统和非 microsoft 的 Web 服务器中。

- **与 Pure Servlets 相比：** 与用大量的 println 语句生成 HTML 相比，JSP 能够更方便的写(和修改!)常规的 HTML。

- **与Server-Side Includes(SSI)相比：** SSI 只是用于简单的包含物，而不是用于使用表单数据、创建数据库链接等的“真正的”程序。

- **与JavaScript相比：** JavaScript 可以在客户端动态地生成 HTML，但很难与 web 服务器交互来执行复杂的任务，如数据库访问、图像处理等。

- **与Static HTML相比：** 当然，常规的 HTML 不能包含动态的信息。

## 后续内容

我将带你一步一步配置环境来开始 JSP 的学习。我假设你有良好的 Java 编程基础来进行 JSP 的学习。

如果你不知道 Java 编程语言，我建议你通过 [Java 教程]( http://www.tutorialspoint.com/java/index.htm)来了解 Java 编程。
