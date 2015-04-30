# JSP——快速指南

## 什么是 JavaServer Pages？ 

JavaServer Pages(JSP) 是一项支持动态内容的 Web 网页的开发技术，它可以帮助开发人员通过利用特殊的 JSP 标签在 HTML 页面中插入Java代码，这些标签大部分都是以 <% 和 %> 为开始。

一个 JavaServer Pages 组件是 Java Servlet 的一种类型，它的作用是可以为一个 Java web 应用程序设计实现一个用户界面。 Web 开发人员结合 HTML 或者 XHTML 代码、XML 元素和嵌入式的 JSP 操作和指令，将 JSP 页面作为文本文件进行编写。

使用 JSP，你可以通过 web 网页的形式收集来自用户的输入，从一个数据库或者另外一个来源呈现记录，并且还可以动态地创建 web 页面。

JSP 标签可以被用于多种用途，例如可以通过数据库或者注册用户的首选项来检索信息，访问 Javabeans 组件，页面之间传递控制指令，请求或页面之间的信息共享等。

## 为什么使用 JSP ？ 

JavaServer Pages 常常使用 Common Gateway Interface (CGI) 使得程序的实现达到相同的目的。但是，和 CGI 相比，JSP 提供了以下几个优势。

- 因为 JSP 允许在 HTML页面本身中嵌入动态元素而不是使用一个单独的 CGI 文件，所以性能明显更好一点。

- JSP 在被服务器处理之前总会被编译一次，它不像 CGI/Perl 那样，每一次页面被请求时，服务器都需要加载一个解释器和目标脚本。

- JavaServer Pages 是在 Java Servlets API 之上创建的，所以 JSP 可以像 Servlets那样也可以访问所有强大的企业级的 Java APIs，包括 JDBC，JNDI，EJB，JAXP 等等。

- JSP 页面可以结合 servlets 进行使用，处理业务逻辑，该模型是通过 Java servlet 模板引擎支持的。

最后，JSP 是 J2EE 中必不可少的一部分，一个完整的企业级应用平台。这意味着 JSP 可以在从最简单到最复杂最苛刻的应用中扮演一个重要的角色。

## 配置 JSP 环境 

这一步涉及到下载一个 Java 软件开发工具包（SDK）的安装包，并且设置合适的 PATH 环境变量。

你可以从 Oracle 的 Java 网站下载 SDK：[**Java SE Downloads**]( http://www.oracle.com/technetwork/java/javase/downloads/index.html)。

一旦你下载了 Java 安装包，你就可以按照给定的指示进行安装并且设置配置。最后设置 PATH 和 JAVA_HOME 环境变量引用的目录，其中包括 java 和 javac，通常分别是 java_install_dir/bin 和 java_install_dir。

如果你是在 Windows环境下运行，并且将 SDK 安装到 C:\jdk1.5.0_20，你需要将以下代码添加到你的 :\autoexec.bat file文件中。

```
set PATH=C:\jdk1.5.0_20\bin;%PATH%
set JAVA_HOME=C:\jdk1.5.0_20
```

另外，在 Windows NT/2000/XP 系统，你也可以右键单击我的计算机，选择属性，然后高级系统设置，然后选择环境变量。然后，你可以更新 PATH 值，并且按下确定按钮。

在 Unix(Solaris,linux,等) 系统，如果 SDK 安装在 /usr/local/jdk1.5.0_20，并且你使用的是 C shell，那么你应该将以下代码添加到你的  .cshrc file 文件中。

```
setenv PATH /usr/local/jdk1.5.0_20/bin:$PATH
setenv JAVA_HOME /usr/local/jdk1.5.0_20
```

另外，如果你使用的是一个集成开发环境（IDE），像 Borland JBuilder、Ecilpse、IntelliJ IDEA，或者 Sun ONE Studio，编译并运行一个简单的程序来确认一下 IDE 知道了你将 Java 安装的位置。

## 配置 Web 服务器：Tomcat 

许多支持 JavaServer Pages 和 Servlets 开发的 Web 服务器在市场上都可以找到。一些 Web 服务器可以免费下载，Tomcat 就是其中之一。

Apache Tomcat 是JavaServer Pages和 Servlets技术的一个开放源码的软件安装包，它可以作为一个独立的服务器对 JSP 和 Servlets 进行测试，也可以与 Apache Web 服务器进行集成。下面是在您的计算机上安装 Tomcat 的安装步骤：

- 从[http://tomcat.apache.org/]( http://tomcat.apache.org/) 下载最新版本的 Tomcat。

- 一旦你下载了安装包，对其进行解压到一个方便的位置。例如在 Windows 系统上可以放在 C:\apache-tomcat-5.5.29，或者在 Linux/Unix 系统上可以放在 /usr/local/apache-tomcat-5.5.29，创建 CATALINA_HOME 环境变量指向这些位置。

在 Windows 机器上通过执行以下命令来启动 Tomcat：

```
%CATALINA_HOME%\bin\startup.bat
 or
 C:\apache-tomcat-5.5.29\bin\startup.bat
```

在 Unix (Solaris, Linux,等) 机器上通过执行以下命令来启动 Tomcat：

```
$CATALINA_HOME/bin/startup.sh
or
/usr/local/apache-tomcat-5.5.29/bin/startup.sh
```

成功启动之后，默认的 包含 Tomcat 的web 应用程序可以通过访问 **http://localhost:8080/** 进行执行。如果一切都很顺利，那么它将显示如下结果：

![](../images/quickguide1.JPG)

关于配置和运行 Tomcat 的更多信息可以在 included 文档中找到，也可以在 Tomcat web网站上找到：http://tomcat.apache.org

## JSP 处理过程: 

下面的步骤解释如何使用 JSP 在web 服务器上创建 web 网页：

- 作为一个正常的页面，您的流感器发送一个 HTTP 请求到 web 服务器。

- web 服务器确认这个 HTTP 请求是来自一个 JSP 页面的，并将其转发给一个 JSP 引擎。这是通过使用 URL 或者是以 .jsp 而不是 .html 为结尾的 JSP 页面完成的。

- JSP 引擎从从磁盘加载 JSP 页面并将其转换成一个 servlet 目录。这种转换是非常简单的，所有的模板文本都转换为 println() 语句，所有的 JSP 元素被转换成实现页面相应的动态行为的 Java 代码。

- JSP 引擎将 servlet 编译成一个可执行的类，并将原始的请求转发给一个 servlet 引擎。

- Web 服务器的一部分调用 servlet 引擎加载 Servlet 类并执行它。执行期间，servlet 产生一个 HTML 格式的输出，这可以使 servlet 引擎通过一个 HTTP 相应传到 web 服务器。

- Web 服务器通过静态的 HTTP 内容将 HTTP 相应转发到您的浏览器上。

- 最后 web 浏览器处理 HTTP 响应中动态生成的 HTML 页面，就好像它完全是一个静态页面。

上述所有步骤可用下图所示：

![](../images/quickguide2.jpg)

## 脚本程序段: 

一个脚本程序段可以包含任意数量的 JAVA语言的语句、变量或者方法声明，或者是在页面脚本语言有效地表达式。

以下是脚本程序的语法：

```
<% code fragment %>
```

你可以用上面的语法编写 XML 如下：

```
<jsp:scriptlet>
   code fragment
</jsp:scriptlet>
```

你写的任何文本、HTML 标签，或者 JSP 元素必须在脚本程序段之外。以下是 JSP 的第一个简单的例子：

<pre class="prettyprint notranslate">
&lt;html&gt;
&lt;head&gt;&lt;title&gt;Hello World&lt;/title&gt;&lt;/head&gt;
&lt;body&gt;
Hello World!&lt;br/&gt;
&lt;%
out.println("Your IP address is " + request.getRemoteAddr());
%&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


**注：** 假设 Apache Tomcat 安装在 C:\apache-tomcat-7.0.2，并且你是按照环境配置教程进行的环境配置。

让我们将上面的代码保留在 JSP 文件 hello.jsp 中，将这个文件放在 **C:\apache-tomcat-7.0.2\webapps\ROOT** 目录下，通过提供的 URL http://localhost:8080/hello.jsp 尝试浏览它。这将会生成如下图所示的结果：

![](../images/quickguide3.jpg)

## JSP 声明: 

一个声明可以声明一个或者多个变量或者方法，这些变量和方法你可以在后面的 JSP 文件中的 Java 代码里使用。你必须在你使用之前在 JSP 文件中定义这些 变量或方法。

下面是 JSP 声明的语法：

```
<%! declaration; [ declaration; ]+ ... %>
```

你可以使用上面的语法编写 XML 如下：

```
<jsp:declaration>
   code fragment
</jsp:declaration>
```

下面是一个简单的 JSP 声明的示例：

```
<%! int i = 0; %> 
<%! int a, b, c; %> 
<%! Circle a = new Circle(2.0); %> 
```

## JSP 表达式: 

一个 JSP 表达式元素包含一个被求值的脚本语言表达式，转换成一个字符串，并插入到表达式在 JSP 文件中出现的位置。

在 JSP 文件中，因为一个表达式的值被转换成一个字符串，你可以在一行文本中使用一个表达式，不管它是否用 HTML 进行标记。

根据 Java 语言规范，表达式元素可以包含任何有效地表达式，但是你不能使用一个分号来结束一个表达式。

下面是 JSP 表达式的语法：

```
<%= expression %>
```

你可以使用上面的语法编写 XML 如下：

```
<jsp:expression>
   expression
</jsp:expression>
```

下面是一个简单的 JSP 表达式的例子：

<pre class="prettyprint notranslate">
&lt;html&gt; 
&lt;head&gt;&lt;title&gt;A Comment Test&lt;/title&gt;&lt;/head&gt; 
&lt;body&gt;
&lt;p&gt;
   Today's date: &lt;%= (new java.util.Date()).toLocaleString()%&gt;
&lt;/p&gt;
&lt;/body&gt; 
&lt;/html&gt; 
</pre>


这将生成以下结果：

<table  class="table table-bordered" cellpadding="5">
<tr><td>
<p> Today's date: 11-Sep-2010 21:24:25 </p>
</td></tr>
</table>


## JSP 注释: 

JSP 注释标记那些 JSP 容器忽略的文本或语句。当你想要隐藏或者“注释掉”你 JSP 页面的一部分时，一个 JSP 注释是非常有用的。

下面是 JSP 注释的语法：

```
<%-- This is JSP comment --%>
```

下面是一个简单的 JSP 注释的例子：

<pre class="prettyprint notranslate">
&lt;html&gt; 
&lt;head&gt;&lt;title&gt;A Comment Test&lt;/title&gt;&lt;/head&gt; 
&lt;body&gt; 
&lt;h2&gt;A Test of Comments&lt;/h2&gt; 
&lt;%-- This comment will not be visible in the page source --%&gt; 
&lt;/body&gt; 
&lt;/html&gt; 
</pre>


这将生成以下的结果：

<table  class="table table-bordered" cellpadding="5">
<tr><td>
<h2>A Test of Comments</h2>  
</td></tr>
</table>


有少量的特殊结构，你可以在几种情况下插入注释或者字符，否则将被特殊对待。这里是一个总结： 

<table class="table table-bordered">
<tr><th style="width:35%">语法 </th><th>目的 </th></tr>
<tr><td>&lt;%-- 注释 --%&gt;</td><td>一个 JSP 注释。被 JSP 引擎所忽略。</td></tr>
<tr><td>&lt;!—注释 --&gt;</td><td>一个 HTML注释。被浏览器忽略。</td></tr>
<tr><td>&lt;\%</td><td>静态的 &lt;% 文字.</td></tr>
<tr><td>%\&gt;</td><td>静态的 %&gt; 文字.</td></tr>
<tr><td>\'</td><td>单引号，在一个属性中使用单引号。</td></tr>
<tr><td>\"</td><td>双引号，在一个属性中使用双引号。</td></tr>
</table>

## JSP 指令:  

一个 JSP 指令影响着 servlet 类的总体结构。它通常具有以下形式：

```
<%@ directive attribute="value" %>
```

有三种类型的指令标签：

<table class="table table-bordered">
<tr><th style="width:40%"> 指令 </th><th>描述 </th></tr>
<tr><td>&lt;%@ page ... %&gt;</td><td>定义 page-dependent 属性，例如脚本语言、错误页面、和缓冲需求。</td></tr>
<tr><td>&lt;%@ include ... %&gt;</td><td>在翻译阶段包含一个文件。</td></tr>
<tr><td>&lt;%@ taglib ... %&gt;</td><td>声明一个标签库，包含在页面中使用的自定义动作。</td></tr>
</table>

我们将在不同的章节中解释 JSP 指令[**JSP - Directives**]( http://www.tutorialspoint.com/jsp/jsp_directives.htm)。

## JSP 动作: 

JSP 动作使用 XML 语法结构来控制 servlet 引擎的行为。你可以动态插入一个文件、重用 JavaBeans 组件、转发用户到另一个网页，或者为 Java 插件生成 HTML。

因为动作元素符合 XML 标准，所以它只有一个语法：

```
<jsp:action_name attribute="value" />
```

动作元素基本上是预定义的函数，以下是可用的 JSP 动作：

<table class="table table-bordered">
<tr><th style="width:30%">语法 </th><th>目的 </th></tr>
<tr><td>jsp:include</td><td>页面被请求时包含包含一个文件</td></tr>
<tr><td>jsp:include</td><td>页面被请求时包含包含一个文件</td></tr>
<tr><td>jsp:useBean</td><td>找到或实现一个 JavaBean 对象</td></tr>
<tr><td>jsp:setProperty</td><td>设置一个 JavaBean 的属性</td></tr>
<tr><td>jsp:getProperty</td><td>将一个 JavaBean 的属性插入到输出</td></tr>
<tr><td>jsp:forward</td><td>将请求转发给一个新页面</td></tr>
<tr><td>jsp:plugin</td><td>生成浏览器特定代码，使得一个OBJECT 或EMBED 标签生成 Java 插件</td></tr>
<tr><td>jsp:element</td><td>动态定义 XML 元素。</td></tr>
<tr><td>jsp:attribute</td><td>定义了动态定义的 XML 元素的属性。</td></tr>
<tr><td>jsp:body</td><td>定义了动态定义的 XML 元素的正文。</td></tr>
<tr><td>jsp:text</td><td>用于在 JSP 页面和文档中编写模板文本。</td></tr>
</table>

我们将在不同的章节中解释 JSP 动作[JSP - Actions]( http://www.tutorialspoint.com/jsp/jsp_actions.htm)。

## JSP 隐式对象: 

JSP 支持9种自定义的变量，它们也被称为隐式对象。这些变量是：

<table class="table table-bordered">
<tr><th style="width:30%">对象 </th><th>描述</th></tr>
<tr><td>request</td><td>这是 <b>HttpServletRequest</b> 对象，与请求相关联。</td></tr>
<tr><td>response</td><td>这是 <b>HttpServletResponse</b> 对象，与客户端响应相关联。</td></tr>
<tr><td>out</td><td>这是 <b>PrintWriter</b> 对象，用于将输出发送到客户端。</td></tr>
<tr><td>session</td><td>这是 <b>HttpSession</b> 对象，与请求相关联。</td></tr>
<tr><td>application</td><td>这是 <b>ServletContext</b> 对象，与应用程序上下文有关。</td></tr>
<tr><td>config</td><td>这是 <b>ServletConfig</b> 对象，与页面相关联。</td></tr>
<tr><td>pageContext</td><td>这将服务器特定属性封装使用，就像高性能的<b>JspWriters</b>。</td></tr>
<tr><td>page</td><td>它与 <b>this</b> 是一个简单的同义词,被用来调用通过翻译的 servlet 类定义的方法。</td></tr>
<tr><td>Exception</td><td>该 <b>Exception</b> 对象允许异常数据被指定的 JSP 访问。</td></tr>
</table>

我们将在不同的章节中解释 JSP 隐式对象[**JSP - Implicit Objects**]( http://www.tutorialspoint.com/jsp/jsp_implicit_objects.htm)。

## 控制流语句:

JSP 提供了强有力的 Java 来嵌入到你的 web 应用程序中。你可以在你的 JSP 编程中使用 Java 所有的 APIs 和 构建模块，包括决策语句、循环等。

## 决策语句: 

**If…else** 块开始像一个普通的脚本，但是脚本在每一行是用 HTML 文本封闭的，包含在脚本标签之间的。

<pre class="prettyprint notranslate">
&lt;%! int day = 3; %&gt; 
&lt;html&gt; 
&lt;head&gt;&lt;title&gt;IF...ELSE Example&lt;/title&gt;&lt;/head&gt; 
&lt;body&gt;
&lt;% if (day == 1 | day == 7) { %&gt;
      &lt;p&gt; Today is weekend&lt;/p&gt;
&lt;% } else { %&gt;
      &lt;p&gt; Today is not weekend&lt;/p&gt;
&lt;% } %&gt;
&lt;/body&gt; 
&lt;/html&gt; 
</pre>


这将产生以下的结果：

<table  class="table table-bordered" cellpadding="5">
<tr><td>
<p> Today is not weekend</p>
</td></tr>
</table>


现在看看下面的 **switch…case** 块，在脚本内，它通过使用 **out.println()** 写出不同的值：

<pre class="prettyprint notranslate">
&lt;%! int day = 3; %&gt; 
&lt;html&gt; 
&lt;head&gt;&lt;title&gt;SWITCH...CASE Example&lt;/title&gt;&lt;/head&gt; 
&lt;body&gt;
&lt;% 
switch(day) {
case 0:
   out.println("It\'s Sunday.");
   break;
case 1:
   out.println("It\'s Monday.");
   break;
case 2:
   out.println("It\'s Tuesday.");
   break;
case 3:
   out.println("It\'s Wednesday.");
   break;
case 4:
   out.println("It\'s Thursday.");
   break;
case 5:
   out.println("It\'s Friday.");
   break;
default:
   out.println("It's Saturday.");
}
%&gt;
&lt;/body&gt; 
&lt;/html&gt; 
</pre>


这将产生以下结果：

<table  class="table table-bordered" cellpadding="5">
<tr><td>
<p>It's Wednesday.</p>
</td></tr>
</table>

## 循环语句: 

在你的 JSP 编程中你也可以使用 Java 中的三种基本的循环类型：**for, while,and do.while** 块。

让我们看看下面的 **for** 循环的例子：

<pre class="prettyprint notranslate">
&lt;%! int fontSize; %&gt; 
&lt;html&gt; 
&lt;head&gt;&lt;title&gt;FOR LOOP Example&lt;/title&gt;&lt;/head&gt; 
&lt;body&gt;
&lt;%for ( fontSize = 1; fontSize &lt;= 3; fontSize++){ %&gt;
   &lt;font color="green" size="&lt;%= fontSize %&gt;"&gt;
    JSP Tutorial
   &lt;/font&gt;&lt;br /&gt;
&lt;%}%&gt;
&lt;/body&gt; 
&lt;/html&gt; 
</pre>


这将产生以下结果：

<table class="table table-bordered" cellpadding="5">
<tr><td>
   <font color="green" size="1">
    JSP Tutorial
   </font><br />
    <font color="green" size="2">
    JSP Tutorial
   </font><br />
    <font color="green" size="3">
    JSP Tutorial
   </font><br />
</td></tr>
</table>


上面的例子可以用 **while** 循环写成如下形式：

<pre class="prettyprint notranslate">
&lt;%! int fontSize; %&gt; 
&lt;html&gt; 
&lt;head&gt;&lt;title&gt;WHILE LOOP Example&lt;/title&gt;&lt;/head&gt; 
&lt;body&gt;
&lt;%while ( fontSize &lt;= 3){ %&gt;
   &lt;font color="green" size="&lt;%= fontSize %&gt;"&gt;
    JSP Tutorial
   &lt;/font&gt;&lt;br /&gt;
&lt;%fontSize++;%&gt;
&lt;%}%&gt;
&lt;/body&gt; 
&lt;/html&gt; 
</pre>


这将产生以下结果：

<table  class="table table-bordered" cellpadding="5">
<tr><td>
   <font color="green" size="1">
    JSP Tutorial
   </font><br />
    <font color="green" size="2">
    JSP Tutorial
   </font><br />
    <font color="green" size="3">
    JSP Tutorial
   </font><br />
</td></tr>
</table>

## JSP 运算符: 

JSP 支持所有的在 Java 中支持的逻辑和算术运算符。下表给出所有运算符的列表，优先级最高的运算符出现在表的顶部，那些优先级低的运算符出现在表的底部。

在一个表达式中，优先级高的运算符会被优先计算。

<table class="table table-bordered">
<tr> <th>类别&nbsp;</th> <th>运算符&nbsp;</th>
<th>关联性&nbsp;</th> </tr> <tr> <td>Postfix&nbsp;</td>
<td>() [] . (点运算符)</td> <td>从左到右&nbsp;</td> </tr> <tr> <td>Unary&nbsp;</td> 
<td>++ - - !  ~ </td> <td>从右到左&nbsp;</td>
</tr> <tr> <td>Multiplicative &nbsp;</td> <td>*  /  %&nbsp;</td>
<td>从左到右&nbsp;</td> </tr> <tr> <td>Additive &nbsp;</td>
<td>+  -&nbsp;</td> <td>从左到右&nbsp;</td> </tr>
<tr> <td>Shift &nbsp;</td> <td>&gt;&gt; &gt;&gt;&gt; &lt;&lt; &nbsp;</td> <td>从左到右&nbsp;</td> </tr> <tr> <td>Relational &nbsp;</td>
<td>&gt; &gt;=  &lt; &lt;= &nbsp;</td> <td>从左到右&nbsp;</td> </tr>
<tr> <td>Equality &nbsp;</td> <td>==  !=&nbsp;</td> <td>从左到右&nbsp;</td> </tr> <tr> 
<td>Bitwise AND&nbsp;</td>
<td>&amp;&nbsp;</td> <td>从左到右&nbsp;</td> </tr> <tr> <td>Bitwise
XOR&nbsp;</td> <td>^&nbsp;</td> <td>从左到右&nbsp;</td>
</tr> <tr> <td>Bitwise OR&nbsp;</td> <td>|&nbsp;</td> <td>从左到右&nbsp;</td> </tr> <tr> <td>Logical AND&nbsp;</td>
<td>&amp;&amp;&nbsp;</td> <td>从左到右&nbsp;</td> </tr> <tr>
<td>Logical OR&nbsp;</td> <td>||&nbsp;</td> <td>从左到右&nbsp;</td> </tr> <tr> <td>Conditional&nbsp;</td>
<td>?:&nbsp;</td> <td>从右到左&nbsp;</td> </tr> <tr>
<td>Assignment&nbsp;</td> <td>=  +=  -=  *=  /=  %=
&gt;&gt;=  &lt;&lt;=  &amp;=  ^=   |=&nbsp;</td> <td>从右到左&nbsp;</td>
</tr> <tr> <td>Comma&nbsp;</td> <td>,&nbsp;</td> <td>从左到右&nbsp;</td> </tr> </table>

## JSP 字面值:  

JSP 表达式语言定义了一下字面值：

-	**Boolean**：真和假

-	**Integer**：同 Java

-	**Floating point**：同 Java

-	**String**：使用单引号和双引号；" 转义为 \"， ' 转义为 \'， \ 转义为 \\

-	**Null**:空









