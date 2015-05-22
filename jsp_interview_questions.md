# JSP - 面试问题 

亲爱的读者，这些 **JSP 面试问题**是专门设计来让你了解问题的本质的，而这些问题都是在你面试时对 **JSP** 主题可能遇到的。根据我的经验，在你面试的过程中，好的面试官并不打算问你任何特殊的问题，通常的问题是以一些基本的概念为开始的，而后他们会继续在之前的基础上进行进一步的讨论以及你的回答：

## 问：什么是 JSP？

**答：**JavaServer Pages(JSP) 是一项支持动态内容的 Web 网页的开发技术，它可以帮助开发人员通过利用特殊的 JSP 标签在 HTML 页面中插入Java代码，这些标签大部分都是以 <% 和 %> 为开始。

## 问：使用 JSP 的优点是什么？

**答：**JSP 提供了如下所列的几个优势：

- 因为 JSP 允许在 HTML页面本身中嵌入动态元素而不是使用一个单独的 CGI 文件，所以性能明显更好一点。
- JSP 在被服务器处理之前总会被编译一次，它不像 CGI/Perl 那样，每一次页面被请求时，服务器都需要加载一个解释器和目标脚本。
- JavaServer Pages 是在 Java Servlets API 之上创建的，所以 JSP 可以像 Servlets那样也可以访问所有强大的企业级的 Java APIs，包括 JDBC，JNDI，EJB，JAXP 等等。
- JSP 页面可以结合 servlets 进行使用，处理业务逻辑，该模型是通过 Java servlet 模板引擎支持的。

## 问：和 ASP 相比，JSP 的优势是什么？

**答：**JSP 的优势是双重的。

首先，动态的部分是用 Java 中编写的，而不是 Visual Basic 或者其他 MS 特定的语言，所以它用来更强大也更容易。

其次，它可以很方便的移植到其他操作系统，并且是非微软 web 服务器。

## 问：和单纯的 Servlets 相比，JSP 的优势是什么？

**答：**与通过使用大量的 println 语句生成的 HTML 相比，JSP 在编写（和修改）常规的 HTML上更方便。其他的优点是：

- 在 HTML 页面中嵌入 Java 代码。
- 跨平台。
- 创建数据库驱动的 web 应用程序。
- 服务器端的编程功能。

## 问：和服务器端包含（SSI）相比，JSP 的优势是什么？

**答：**SSI 只是用于简单的包裹体，而不是用于“真正的”使用表格数据的应用程序，建立数据库连接，等等。

## 问：和 JavaScript 相比，JSP 的优势是什么？

**答：**JavaScript 可以在客户端生成动态的 HTML，却不能和 web 服务器进行交互来完成复杂的任务，例如数据库的访问和图像处理等等。

## 问：和静态 HTML 相比，JSP 的优势是什么？

**答：**当然，常规的 HTML 不能包含动态信息。

## 问：解释一个 JSP 的生命周期。

**答：**一个 JSP 的生命周期包含以下步骤：

- **编译：**当浏览器请求一个 JSP 时，JSP 引擎首先检查是否需要编译这个页面。如果这个页面从来没有被编译过，或者 JSP 在最后一次被编译后已经被修改了，那么 JSP 引擎会编译这个页面。

	编译过程包括三个步骤：

	- 解析 JSP。
	- 将 JSP 转换成一个 servlet。
	- 编译这个 servlet。

- **初始化：**当一个容器加载一个 JSP 时，在修改任何请求之前会调用 jsInit() 方法。
- **执行：**无论何时一个浏览器请求一个 JSP 时，这个页面都会被加载并且初始化，JSP 引擎在 JSP 中调用 _jspService() 方法。一个 JSP 的 _jspService() 方法在每一次请求时都会被调用，并且为该请求负责生成响应，该方法还负责生成所有的7个 HTTP 方法的响应，也就是 GET， POST，DELETE 等等。
- **清除：**当一个 JSP 被一个容器从应用中移除时是 JSP 生命周期的破坏阶段。jspDestroy() 方法相当于 servlets 中的销毁方法。

## 问：在 JSP 中一个 sciptlet 是什么？它的语法是什么？

**答：**一个 sciptlet 可以包含任意数量的 JAVA 语言的语句、变量或者方法声明，或者在页面脚本语言中有效地表达式。

Scriptlet 的语法如下：

```
<% code fragment %>
```

## 问：什么是 JSP声明？

**答：**一个声明可以声明一个或者多个变量或者方法，这些变量和方法你可以在后面的 JSP 文件中的 Java 代码里使用。你必须在你使用之前在 JSP 文件中定义这些 变量或方法。

```
<%! declaration; [ declaration; ]+ ... %>
```

## 问：什么是 JSP 表达式？

**答：**一个 JSP 表达式元素包含一个被求值的脚本语言表达式，转换成一个字符串，并插入到表达式在 JSP 文件中出现的位置。

根据 Java 语言规范，表达式元素可以包含任何有效地表达式，但是你不能使用一个分号来结束一个表达式。

它的语法是：

```
<%= expression %>
```

## 问：什么是 JSP 注释？

**答：**JSP 注释标记的是 JSP容器忽略的文本或者语句。一个 JSP 注释在你想要隐藏或者“注释掉”你 JSP 页面的一部分时是很有用的。

下面的 JSP 注释的语法：

```
<%-- This is JSP comment --%>
```

## 问：什么是 JSP 指令？

**答：**一个 JSP 指令影响着 servlet 类的总体结构。它通常具有以下形式：

```
<%@ directive attribute="value" %>
```

## 问：指令标签的类型是什么？

**答：**指令标签的类型如下：

- **<%@ page ... %> :** 定义 page-dependent 属性，例如脚本语言、错误页面、和缓冲需求。
- **<%@ include ... %> :** 在翻译阶段包含一个文件。
- **<%@ taglib ... %> :** 声明一个标签库，包含在页面中使用的自定义动作。

## 问：什么是 JSP 操作？

**答：**JSP 操作使用 XML 语法结构来控制 servlet 引擎的行为。你可以动态插入一个文件、重用 JavaBeans 组件、转发用户到另一个网页，或者为 Java 插件生成 HTML。

它的语法如下：

```
<jsp:action_name attribute="value" />
```

## 问：一些 JSP 操作的名称？

**答：**jsp:include， jsp:useBean， jsp:setProperty， jsp:getProperty， jsp:forward， jsp:plugin，jsp:element， jsp:attribute， jsp:body， jsp:text

## 问：什么是 JSP 字面值？

**答：**字面值是一些值，例如一个数字或者一个文本字符串，编写程序代码的一部分。JSP 表达式语言定义以下字面值：

- **Boolean：**真和假
- **Integer：**同 Java
- **Floating point：**同 Java
- **String：**使用单引号和双引号；" is escaped as \", ' is escaped as \', and \ is escaped as \\
- **Null:**空

## 问：什么是页面指令？

**答：****页面**指令用于为属于当前 JSP 页面的容器提供指示。你可能会在你的 JSP 页面的任何位置编写页面指令。

## 问：页面指令的各种属性是什么？

**答：**页面指令包含以下13个属性。

1. language
2. extends
3. import
4. session
5. isThreadSafe
6. info
7. errorPage
8. isErrorpage
9. contentType
10. isELIgnored
11. buffer
12. autoFlush
13. isScriptingEnabled

## 问：一个缓冲的属性是什么？

**答：**缓冲属性为服务器输出响应对象指定缓冲特性。

## 问：当缓冲区设置为“空”时，发生了什么？

**答：**当缓冲区设置为“空”时，servlet 输出会直接定向到响应输出对象。

## 问：什么是 autoFlush 属性？

**答：**当一个缓冲区已满时，**autoFlush** 属性会指定缓冲输出是否会被自动溢出，还是应该抛出一个异常来指示缓冲区已满。

**真**（默认）值说明自动缓冲溢出，**假**值将抛出一个异常。

## 问：什么是 contentType 属性？

**答：contentType** 属性为 JSP 页面和生成的响应页面设置字符编码。默认的内容类型是 text/html，这是 HTML 页面里标准的内容类型。

## 问：什么是 errorPage 属性？

**答：**如果当前运行的页面中有一个错误的话，**errorPage** 属性通知 JSP 引擎显示的是哪一个页面。errorPage 属性的值是相对的 URL。

## 问：什么是 isErrorPage 属性？

**答：**isErrorPage 属性表明当前的 JSP 可以被另一个页面用于错误页面。
isErrorPage 的值不是真就是假。isErrorPage 属性的默认值是假。

## 问：什么是 extends 属性？

**答：extends** 属性指定一个超级类，该类中生成的 servlet 必须被扩展。

## 问：什么是 import 属性？

**答：import** 属性和 Java 导入语句有着相同的作用和表现。导入选项的值是你想要导入的包的名称。

## 什么是 info 属性？  

**答：info** 属性让你提供对 JSP 的描述。

## 什么是 isThreadSafe 属性？  

**答：isThreadSafe** 选项标志着一个页面是线程安全的。默认情况下，所有的 JSPS 都被认为是线程安全的。如果你设置 isThreadSafe 选项的值为假，JSP引擎确保一次只有一个线程在执行你的 JSP。

## 什么是 language 属性？  

**答：language** 属性表明在 JSP 脚本语言中使用的编程语言。

## 什么是 session 属性？  

**答：session** 属性表明 JSP 页面使用的是否是 HTTP 会话。真值意味着 JSP 页面有权访问一个内置命令的会话对象，假值则意味着 JSP 页面无权访问内置命令的会话对象。

## 什么是 isElIgnored 属性？  

**答：isElIgnored** 选项使你可以禁用表达式语言（EL）表达式的值。该属性的默认值为真，意味着表达式 ${...} 的值是由 JSP 规范决定的。如果属性的值设置为假，那么表达式不会被赋值而是被认为是静态文本。

## 什么是 isScriptingEnabled 属性？  

**答：isScriptingEnabled** 属性决定是否允许使用脚本元素。

默认值（真）可以使用脚本片段、表达式，和声明。如果这个属性值被设置为假，如果 JSP 使用任何脚本片段、表达式（non-EL），或者声明，那么将会出现一个 translation-time 错误。

## 什么是一个 include 命令？  

**答：**包含命令被用于在翻译阶段包含一个文件。这个指令告诉容器在翻译阶段将当前的 JSP和其他外部文件的内容进行合并。你可以在你的 JSP页面的任何位置编写包含指令。

一般使用该指令是形式如下：

```
<%@ include file="relative url" >
```

## 什么是一个 taglib 指令？  

**答：**taglib 指令遵循以下语法：

```
<%@ taglib uri="uri" prefix="prefixOfTag">
```

Uri 属性值解析一个容器理解的位置。

Prefix 属性通知一个容器标记位是一个自定义动作。

Taglib 指令遵循以下语法：

```
<%@ taglib uri="uri" prefix="prefixOfTag">
```

## 在动作元素中 id 和 scope 属性的意义是什么？  

**答：**

- **ID 属性：**id 属性唯一的标识动作元素，允许在 JSP 页面中引用动作。如果动作创建一个对象的实例，id 值可以通过隐式对象 PageContext 对它进行引用。
- **Scope 属性：**这个属性标识动作元素的生命周期。Id 属性和 scope 属性是直接相关的，scope 属性决定了与 id 属性相关的对象的寿命。scope 属性有四个可能的值：（a）页面，（b）请求，（c）会话，和（d）应用程序。

## `<jsp:include>` 动作的功能是什么？  

**答：**该操作允许你将文件插入到生成的页面中。语法如下：

```
<jsp:include page="relative URL" flush="true" />
```

其中，**page** 是页面中包含的相对应的 URL。

**Flush** 是一个布尔型的属性，决定被包含的资源在被包含之前它的缓冲区是否被刷新。

## include 操作和 include 指令之间的区别是什么？  

**答：include 指令**是在 JSP 页面被翻译成一个 servlet 时插入一个文件，而**include 操作**是在页面被请求使插入文件。

## 什么是 `<jsp:useBean>` 操作？  

**答：useBean** 操作是非常通用的。它首先利用 id 和 scope 变量搜索一个现有的对象。如果没有找到一个对象，那么它试图创建一个指定的对象。

加载一个 bean 最简单的方法如下：

```
<jsp:useBean id="name" class="package.class" />
```

## 什么是 `<jsp:setProperty>` 操作？  

**答：setProperty** 操作设置一个 Bean 的属性。Bean 必须在该操作之前被定义。

## 什么是 `<jsp:getProperty> 操作？  

**答：getProperty** 操作被用于检索一个给定的属性值，并且将其转换为一个字符串，最后将它插入到输出。

## 什么是 `<jsp:forward>` 操作？  

**答：forward** 操作终止当前的页面，并将请求转发给另一个资源，例如一个静态页面、另一个 JSP 页面，或者一个 Java Servlet。

该操作的一个简单的语法如下：

```
<jsp:forward page="Relative URL" />
```

## 什么是 `<jsp:plugin>` 操作？  

**答：plugin** 操作用于将 Java 组件插入到一个 JSP 页面。它决定了浏览器的类型和需要插入的 <object> 或者 <embed> 标签。

如果所需要的插件不存在，下载插件，然后执行 Java 组件。Java 组件可以是一个 Applet 或者是一个 JavaBean。

## JSP 操作不同的 scope 值是什么？  

**答：**scope 属性标识了一个动作元素的生命周期。它有四个可能的值：（a）页面，（b）请求，（c）会话，和（d）应用程序。

## 什么是 JSP 隐式对象？  

**答：**JSP 隐式对象是在每一个页面中 JSP 容器为开发人员提供的可用的 Java 对象，开发人员可以直接调用它们，而不需要显式的声明。JSP 隐式对象还被称为预定义的变量。

## JSP 支持的隐式对象是什么？  

**答：**request， response， out,session， application， config， pageContext， page， Exception。

## 什么是 request 对象？  

**答：**request 对象是 javax.servlet.http.HttpServletRequest 对象的一个实例。每次客户端请求一个页面时，JSP 引擎都会创建一个新的对象来表示这个请求。

request 对象为获取 HTTP 头信息提供方法，这些头信息包括表单数据、 cookie、 HTTP 方法等等。

## 你如何读取一个请求的头信息？  

**答：**使用HttpServletRequest 的 getHeaderNames() 方法来读取 HTTP 头信息。该方法返回一个枚举，包含与当前请求相关的头信息。

## 什么是一个 response 对象？  

**答：**response 对象是 javax.servlet.http.HttpServletRequest 对象的一个实例。正如服务器创建请求对象，它还创建了一个对象来表示对客户端的响应。

response 对象还定义了处理创建新的 HTTP 头的接口。通过这个对象，JSP 程序员可以添加新的 cookies 或者日期戳， HTTP 状态码等等。

## 什么是外部隐式对象？  

**答：外部**隐式对象是 javax.servlet.jsp.JspWriter 对象的一个实例，它被用于在一个响应里发送内容。

## JspWriter 和 PrintWriter 的区别是什么？  

**答：****JspWriter** 对象包含大部分与 java.io.PrintWriter 相同的方法。然而，JspWriter 有一些额外的方法用来处理缓冲。和 PrintWriter 对象不同，JspWriter 抛出 IOExceptions 异常。

## 什么是 session 对象？  

**答：**session 对象是 javax.servlet.http.HttpSession 的一个实例，它被用于在客户端请求之间跟踪客户端会话。

## 什么是一个应用程序对象？  

**答：**应用程序对象是为生成的 Servlet 围绕 ServletContext 对象的直接包装器，实际上是 javax.servlet.ServletContxet 对象的一个实例。

这个对象是 JSP 页面的在整个生命周期上的一个表示。该对象的创建是在 JSP 页面初始化的时候，并且是在 JSP 页面被删除时通过 JSPDestroy() 方法删除的。

## 什么是一个 config 对象？  

**答：**config 对象是 javax.servlet.ServletConfig 的一个实例，是为生成的 Servlet 围绕 ServletConfig 对象的直接包装器。

该对象允许 JSP 程序员有权访问 Servlet 或者 JSP 引擎初始化参数，比如路径或文件位置等等。

## 什么是一个 pageContext 对象？  

**答：**pageContext 对象是 javax.servlet.jsp.PageContext 对象的一个实例。pageContext 对象被用于表示整个 JSP 页面。

该对象存储每一个请求的请求和响应对象的引用。应用程序、配置、会话，和外部对象的派生是通过访问该对象的属性生成的。

pageContext 对象还包含发送给 JSP 页面的指令的信息，包括缓冲信息、错误的页面 URL，和页面范围。

## 什么是一个 page 对象？  

**答：**该对象实际上是对页面实例的一个真正的引用。它可以被认为是一个表示整个 JSP 页面的一个对象。

Page 对象实际上是这个对象的一个直接的同义词。

## 什么是一个 exception 对象？  

**答：**exception 对象是一个包装器，包含从上一个页面抛出的异常。它通常用于生成一个适当的错误条件的响应。

## 在 HTTP 协议中 GET 和 POST 的区别？  

**答：**GET 方法发送添加到页面请求的编码后的用户信息。页面和编码信息是通过？符号分开的。

POST 方法将信息打包的方式与 GET 方法时一样的，但是而是将它放在 URL 中？的后面作为文本字符串进行发送，将它作为一个独立的消息发送。该消息来自后台程序的标准输入，在你的处理过程中可以解析和处理它。

## 如何使用 JSP 读取 表单数据？  

**答：**JSP根据情况自动解析并使用下面的方法处理表单数据：

- **getParameter()：**调用 request.getParameter() 方法来获取一个表单参数的值。
- **getParameterValues()：**如果参数出现多次，调用该方法，返回多个值，例如复选框。
- **getParameterNames()：**在当前的请求中，如果你想要一个完整的所有的参数列表，调用该方法。
- **getInputStream()：**调用该方法来读取来自客户端的二进制数据流。

## 什么是过滤器？  

**答：**JSP 过滤器是 Java 类，它可以用于 JSP 编程中的以下目的：

- 它们在后台访问一个资源之前，拦截来自客户端的请求。
- 在它们将响应发送回客户端之前操作来自服务器的响应。

## 任何定义过滤器？  

**答：**过滤器是在部署描述文件 web.xml 中定义的，然后映射到你的应用程序的部署描述文件的 servlet 或者 JSP 名称 或者 URL 模式。

当 JSP 容器启动 web 应用程序时，它创建一个过滤器的实例，该实例已经在部署描述文件中声明过了。过滤器按照他们在部署描述文件中声明的顺序执行。

## 什么是 cookies？  

**答：**Cookies 是存储在客户端计算机的文本文件，它们保存各种跟踪目的的信息。

## cookies 是如何工作的？  

**答：**Cookies 通常放置在一个 HTTP 的头部（尽管在浏览器上 JavaScript 也可以直接设置一个 cookie）。如果浏览器已经配置可以存储 cookies，那么它将保存信息直到截止日期。如果用户点击浏览器的任意页面，那么会为之匹配 cookie 的路径和区域，它将重新将 cookie 发送到服务器。

## 在 JSP 中如何设置 cookies？  

**答：**在 JSP 中设置 cookies 包含三个步骤：

- **创建一个 Cookie 对象：**利用一个 cookie 名称和一个 cookie 值调用 Cookie 的构造函数，两个参数都是字符串型。
- **设置最大年龄：**使用 setMaxAge 指定 cookie 的有效期（以秒为单位）。
- **将 cookie 发送到 HTTP 响应头：**使用 response.addCookie 将 cookie 添加到 HTTP 响应头。


## 在 JSP 中如何读取 cookies？  

**答：**为了读取 cookies，你需要通过调用HttpServletRequest 的 getCookies() 方法来创建一个 javax.servlet.http.Cookie 对象的数组。然后循环数组，利用 getName() 和 getValue() 方法来访问每一个和值相关的 cookie。

## 在 JSP 中如何删除 cookies？  

**答：**删除 cookies 是非常简单的。如果你想要删除一个 cookie，那么你只需要遵从以下三个步骤：

- 读取一个已经存在的 cookie，并将它存储在 Cookie对象中。
- 利用 **setMaxAge()** 方法设置 cookie的年龄为0来删除一个已存在的 cookie。
- 将这个 cookie 添加回到响应头部。


## 在 JSP 中会话管理是如何完成的？  

**答：**可以通过以下来完成会话管理：

- **Cookies**：一个 web 服务器可以将每一个 web 客户端作为一个 cookie 分配一个唯一的会话 ID，对于来自客户端的后续请求，它们可以通过使用保存的 cookie 被认可。
- **隐藏表单字段：**一个 web 服务器可以以唯一的会话 ID 发送一个隐藏的 HTTP 表单字段如下所示：
	
	```
	<input type="hidden" name="sessionid" value="12345">
	```

	这意味着当表单被提交时，指定的名称和值将被包含在 GET 和 POST 方法中。
- **URL 重写：**URL 重写的一些额外信息会被添加到 URL 的末尾，用来标识会话。URL 重写在一个 cookie被禁用时是很有用的。
- **会话对象：**JSP 使用 servlet 提供了 HttpSession 的接口，这提供了一种通过多个页面请求或者访问一个网站来存储用户的信息来识别一个用户的方法。

## 如何删除一个会话数据？  

**答：**当你完成了一个用户的会话数据，你有以下几种选择：

- **移除一个特殊的属性：**你可以调用 public void removeAttribute(String name) 方法来删除与一个特殊关键字相关的值。
- **删除整个会话：**你可以调用 public void invalidate() 方法来抛弃整个会话。
- **设置会话超时：**你可以调用 public void setMaxInactiveInterval(int interval) 方法来单独设置会话超时。
- **用户退出登录：**支持 servlet 2.4 的服务器，你可以调用注销客户端在 web 服务器上的登录，所有属于用户的会话都将会失效。
- **web.xml 配置：**如果你使用的是 Tomcat，除了上述方法以外，你可以在 web.xml 里配置会话超时如下所示。


## 如何利用 JSP 上传一个文件？  

**答：**为了上传一个单一的文件你应该使用一个单一的带有属性类型=“file”的 <input .../>标签。为了允许多个文件上传，对名称属性包含多个不同值的输入标签。

## 上传的文件将被存储在哪里？  

**答：**你可以在你的程序中进行硬编码或者使用外部配置添加该目录名称，比如在 web.xml 中的一个 context-parameter。

## 什么是 JSP 页面重导？  

**答：**页面重导通常是在一个文档被移动到一个新的位置时使用，我们需要将客户端发送到这个新的位置或者可能因为负载平衡，或者简单的随机化。

## `<jsp:forword page=...>` 和 `response.sendRedirct(url)` 的区别是什么？  

**答：**<jsp:forword> 元素将包含客户端请求信息的请求对象从一个 JSP 文件转发到另一个文件。只要是在相同的应用程序上下文中对 JSP 文件进行转发，目标文件可以是一个 HTML 文件，另一个 JSP 文件，或者是一个 servlet。

sendRedirect 向浏览器发送 HTTP 临时重定向响应，并且浏览器会向重定向页面创建一个新的请求。

## 什么是网页点击计数？  

**答：**一个点击计数器告诉你关于你网站上的一个特定页面的访问量。

## 在 JSP 中如何实现一个点击计数器？  

**答：**为了实现一个点击计数器，你可以使用与 getAttribute() 和 setAttribute() 方法相关的应用程序隐式对象。

这个对象是 JSP 页面在整个生命周期上的表现。该对象是在 JSP 页面初始化的创建的，并且当 JSP 页面移除的时候通过 jspDestroy() 方法移除的。

## 如何设计完成点击计数器，避免应用程序每次启动时计数数据的丢失？  

**答：**你可以遵循以下步骤：

- 定义一个单一计数的数据库表，让我们说说点击计数。为它设置一个0值。
- 随着每一次点击，读取该表获取点击计数器的值。
- 当显示点击计数器的新值作为所有页面点击数。
- 如果你想要计算所有页面的计数，对所有的页面实现以上逻辑。

## 什么是自动刷新功能？  

**答：**考虑一个页面，在这个页面中显示在线游戏分数、或股票市场地位或者当前的汇率交换比率。所有这些类型的页面，你需要定期使用浏览器中的刷新按钮或者重新加载按钮刷新你的 web 页面。

JSP 通过提供给你一种机制使得这个工作变得容易，该机制是你可以在一个给定的时间间隔后自动刷新 web 网页。

## 在 JSP 中如何实现自动刷新？  

**答：**刷新网页最最简单的方式是使用响应对象的 setInHeader( ) 方法。下面是该方法的原型：	

```
public void setIntHeader(String header, int headerValue)
```

这种方法向浏览器发送回头“刷新”连同一个整型值，这个值可以以秒为单位显示时间间隔。

## 什么是 JSTL？  

**答：**JavaServer 页面标准标签库（JSTL）是一个有用的 JSP 标签的集合，里面封装了很多 JSP 应用程序的核心功能。

JSTL支持常见的、结构性的任务，比如迭代和条件、用于操纵 XML 文档的标签、国际化标签，和 SQL 标签。它还为整合现有的自定义标签和 JSTL标签提供了一个框架。

## JSTL 不同类型的标签有哪些？  

**答：**JSTL 标签的类型有：

- **核心标签**
- **格式化标签**
- **SQL 标签**
- **XML 标签**
- **JSTL 函数**

## `<c:set>` 标签的作用是什么？  

**答：** < c:set>标签是 setProperty 操作的 JSTL-友好版本。该标签非常有用，因为它计算表达式并使用结果来设置 JavaBean 或 java.util.Map 对象的值。

## `<c:remove>` 标签的作用是什么？  

**答：** < c:remove> 标签从指定的范围或发现变量的第一范围中(如果没有指定范围)删除变量。

## `<c:catch>` 标签的作用是什么？  

**答：** < c:catch>标签捕获出现在标签内部的全部 Throwable 并有选择地公开它。它仅仅是用于错误处理或更得体的处理问题。

## `<c:catch>` 标签的作用是什么？  

**答：** < c:if >标签计算一个表达式，当且仅当表达式计算结果为 true 显示其主体内容。

##  `<c:choose>` 标签的作用是什么？  

**答：** < c:choose >的工作方式类似于 Java switch 语句，因为它允许你在许多选择中做出选择。Switch 语句有 case 语句，< c:choose > 标签有 < c:when> 标签。一个 switch 语句有缺省子句来指定一个默认的操作，相同地，< c:choose > 也有<otherwise>作为缺省子句。

## `<c:forEach>`，`<c:forTokens>` 标签的作用是什么？  

**答：** <c:forEach>，<c:forTokens>标签是很好的选择，通过 scriptlet 来嵌入 Java for，while，或 do-while 循环。

##  `<c:param>` 标签的作用是什么？  

**答：** <c:param>标签允许适当的 URL 请求要被 URL 指定的参数，且没有任何必要的URL 编码要求。

##  `<c:redirect>` 标签的作用是什么？  

**答：** < c:redirect >标签通过提供自动 URL 重写将浏览器重定向到另一个 URL，它支持上下文相关的 URL，也支持< c:param >标签。

##  `<c:url>` 标签的作用是什么？  

**答：**  < c:url >标签将 URL 格式化成一个字符串，并将其存储到一个变量中。这个标签在必要时自动执行 URL 重写。

## 什么是 JSTL 格式化标签？  

**答：** JSTL 格式化标签用于格式化和显示文本、日期、时间，编号为国际化 Web 站点。下面包含在你的 JSP 格式库中的语法：

```
<%@ taglib prefix="fmt" 
           uri="http://java.sun.com/jsp/jstl/fmt" %>
```

## 什么是 JSTL SQL 标签？  

**答：** JSTL SQL 标签库为相关的数据库(RDBMSs)交互提供了标签，如 Oracle， mySQL，和 Microsoft SQL Server。

以下是包含在你的 JSP 中的 JSTL SQL 库的语法：

```
<%@ taglib prefix="sql" 
           uri="http://java.sun.com/jsp/jstl/sql" %>
```

## 什么是 JSTL XML 标签？  

**答：** JSTL XML 标签提供了一种以 JSP 为中心创建和操纵 XML 文档的方式。下面是包含在你的 JSP 中的 JSTL XML 库的语法。

```
<%@ taglib prefix="x" 
           uri="http://java.sun.com/jsp/jstl/xml" %>
```

## 什么是 JSP 自定义标签？  

**答：** 自定义标签是一种用户定义的 JSP 语言元素。当一个包含自定义标签的 JSP 页面时转换成一个 servlet时，该标签就会转换为一个对象上的操作，称为标签处理程序。然后当执行 JSP 页面的 servlet 时，Web 容器就会调用这些操作。

## 什么是 JSP 表达式语言吗？  

**答：**JSP表达式语言(EL)可以方便地访问存储在javabean组件中的应用程序的数据。JSP EL允许创建表达式(a)算术和(b)逻辑。一个简单的JSP EL的语法是：

```
${expr}
```

这儿的expr是指定表达式本身。

## 在 JSP EL 对象分别是什么？  

**答：**JSP表达式语言支持下面的隐式对象

- **pageScope：**变量范围是页面范围
- **requestScope：**变量范围是请求范围
- **sessionScope：**变量范围是会话范围
- **applicationScope：**变量范围是应用范围
- **param：**请求参数作为字符串
- **paramValues：**请求参数作为字符串集合
- **headerHTTP：**HTTP请求标头作为字符串
- **headerValues：**HTTP请求标头作为字符串集合
- **initParam：**上下文初始化参数
- **cookie：**Cookie值
- **pageContext：**当前页面的JSP PageContext对象


## 我们如何禁用 EL？  

**答：**我们可以使用页面的指令的isELIgnored属性禁用EL。

```
<%@ page isELIgnored ="true|false" %>
```

如果它是true，当它们出现在静态文本或标签属性时，EL表达式被忽略。如果它是false，EL表达式都由容器进行计算。

## 在一个 JSP 代码中，你可能会遇到的错误类型？  

**答：**

- **Checked异常**：Checked异常是一个异常，这个异常通常是一个用户错误或一个程序员无法预见的问题。例如，如果一个文件被打开，但无法找到该文件，异常会发生。这些异常时不能简单地忽略编译。
- **Runtime异常**：Checked异常是一个异常，这个异常可能本来是程序员可以避免的。与Checked异常相反的是，runtime异常可以在编译的时候忽略。
- **Errors**：这些都不是异常，但所出现的问题超出了用户或程序员的控制。在代码中，错误通常忽略了，因为你很少能做关于错误的任何事。例如，如果一个堆栈溢出发生时，错误将会发生。他们也在编译的时候忽略了。


## 在 JSP 页面如何处理 runtime 异常？  

**答：**我们可以使用页面指令的errorPage属性将有未捕获的runtime异常自动转发到一个错误处理页面。

例如：<%@ page errorPage="error.jsp" %>

在请求处理期间，如果遇到未捕获的异常，它将重定向浏览器到JSP页面error.jsp。error.jsp必须使用指令：<%@ page isErrorPage="true" %>来表明这是一个错误处理页面。

## 什么是国际化？  

**答：**国际化意味着能够为网站提供不同版本的内容，这些内容被翻译成访问者的语言或国家。

## Localiztion 是什么？  

**答：**Localiztion意味着将资源添加到一个适合特定的地理或文化地区的网址，例如印地语翻译成一个网址。

## 什么是语言环境？  

**答：**这是一个特定的文化或地理区域。它通常被称为语言符号，紧随其后的是国家符号，它使用下划线分隔。例如“en_US”表示US的语言环境。

## `<%-- comment --%>` 和 `<!-- comment -->` 的区别是什么？  

**答：**<%-- comment --%>是JSP命令，可以被JSP工具忽视。

< !-- comment -- >是一个HTML命令，可以被浏览器忽略。

## JSP技术是否可扩展？  

**答：**是的。JSP技术是可扩展的，它通过发展自定义操作、装在标签库中的标签。

## 如何在一个JSP页面包含静态文件？  

**答：**应该使用JSP 的include指令包含静态资源。这种方式，在翻译阶段包含只执行一次。请注意，你应该提供一个文件属性的相对URL。尽管你还可以使用动作元素包含静态资源，但这是不明智的，因为每次请求，包含文件被执行。

## JSP页面可以处理HTML表单数据吗？  

**答：**是的。然而，不同于Servlet，你不需要在JSP页面用特定的方法如doGet()和doPost()实现http协议。对于表单输入元素，你可以通过带有脚本小程序或表达式的请求隐式对象获得的数据。

## 你如何成功控制从一个JSP页面到另一个？  

**答：**使用下面的方法来成功控制请求从一个servlet到另一个servlet或一个JSP到另一个JSP：

- 使用RequestDispatcher对象的forward方法完成控制。
- 使用response.sendRedirect方法。


## 可以在JSP页面内使用ServletOutputStream对象吗？  

**答：**不可以。你应该只使用一个JSPWriter对象(给定隐含对象形式)回复客户。

JSPWriter对象可以被视为一种由response.getWriter()返回的流对象的缓冲版本，尽管从实现的角度来看，它不可以实现。

## 什么是页面指令是用来防止JSP页面自动创建一个会话？  

**答：**<%@ page session="false">

## 如何JSP传递信息到包含的JSP？  

**答：**使用<%jsp:param>标签。

## 我们是否可以重写jspInit()，_jspService()和jspDestroy()？  

**答：**jspInit()和jspDestroy()可以重写，_jspService()不可以重写。

## 为什么_jspService()方法以“_”开始，而其他的生命周期方法没有？  

**答：**_jspService()方法将被容器写入，而任何方法都不能被通常以“_”开始写的终端用户重写。这就是为什么我们在任何JSP页面中不重写_jspService()方法。

## 一个JSP页面，include.jsp，含有实例变量“int a”。现在这个页面是静态的被包含在另一个jsp页面中，home.jsp，它也有声明一个实例变量“int a”。home.jsp页面被客户端请求时，会发生什么？  

**答：**它会导致编译错误，因为两个有相同名字的变量不能声明。这是发生是因为，当一个页面被静态包含，被包含的页面整个代码会成为新页面的一部分。这个时候有两种对变量“a”的声明。因此编译错误。

## 如何禁用脚本？  

**答：**通过将配置描述符的scripting-invalid元素设置为true来禁用脚本。它是一个jsp-property-group的子元素。它的有效值是true和false。禁用脚本的语法如下:

```
<jsp-property-group>
   <url-pattern>*.jsp</url-pattern>
   <scripting-invalid>true</scripting-invalid>
</jsp-property-group>
```

## 什么时候使用应用范围？  

**答：**如果我们想使我们的数据在整个应用程序范围内有效，那么我们必须使用应用范围。

## 在JSP中，什么是包含文件的选项？  

**答：**在JSP，我们可以用以下的方法来执行包含：

- **用include指令：**例如：

	```
	<%@ include file=”header.jsp” %>
	```

- **用include动作：**例如：

	```
	<%@ include file=”header.jsp” %>
	```

- **用pageContext隐含对象：**例如：

	```
	<%
     pageContext.include(“/header.jsp”);
	%>
	```

- **用RequestDispatcher对象：**例如：

	```
	<%
	 RequestDispatcher rd = request.getRequestDispatcher(“/header.jsp”);
	  Rd.incliude(request,response);
	%>
	```

## 如何用JSP引擎实例化标签处理程序类的实例？  

**答：**每次在一个JSP页面遇到一个标签时，JSP引擎总是会实例化一个新的标签处理程序实例。一个标签池实例被维护，在可能的情况下重用它们。当遇到一个标签时，JSP引擎将尝试找到一个没有被使用的标签实例，使用相同的，然后再释放它。

## JavaBeans和taglib指令之间的区别是什么?

**答：**javabeans和taglib的基本原理介绍了可重用性。但以下是它们之间的主要区别：

- Taglib用来生成表达元素，而javabean有益于存储信息和状态。
- 使用自定义标签实现动作元素，而javabean用来呈现信息。

## 下一个是什么?

进一步，你可以通过过去的作业你完成了主题，确保你能够自信地说。如果你是新鲜的,那么面试官并不指望你会回答非常复杂的问题,而你必须让你的基础概念很强。

第二，如果你不能回答一些问题，这并不重要。但问题是，无论你说什么，你必须非常自信地回答。所以在面试时要有信心。在tutorialspoint中，我们希望你有一个完美的面试和为你最好的未来而努力。
