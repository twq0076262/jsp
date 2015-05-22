# JSP - 表单处理

当你需要从你的浏览器向 web 服务器传递一些信息并最终将信息返回到你的后端程序时，你一定遇到了很多情况。浏览器使用两种方法将此信息传递给 web 服务器。这些方法是 GET 方法和 POST 方法。

## GET 方法

GET 方法发送添加到页面请求的编码用户信息。页面和编码信息是被符号 ？ 分开的，如下所示：

``` 
http://www.test.com/hello?key1=value1&key2=value2
```

GET 方法是从浏览器向 web 服务器传递信息的默认的方法，它产生一个长字符串出现在浏览器的位置框中。如果你要把密码或其他敏感信息传递到服务器，那么不要使用 GET 方法。

GET 方法有大小限制：在请求字符串中只可以有 1024 个字符。

这些信息是通过使用 QUERY_STRING 标题传递的，并将通过 QUERY_STRING 环境变量被接收，该环境变量可以使用请求对象的 getQueryString() 方法和 getParameter()方法处理。

## POST 方法

通常情况下，将信息传递给后端程序的更可靠的方法是 POST 方法。

该方法打包信息的方法与 GET 方法是完全一样的，但是它不是将信息作为一个文本字符串放在 URL 中的 ？ 符号之后来发送信息，它是把信息作为一个单独的消息来发送该消息。这个消息是以标准输入的形式发送到后端程序的，在你的处理过程中你可以解析并使用这个消息。

JSP 处理这种类型的请求时，使用 getParameter() 方法读取简单参数，使用 getInputStream()方法读取来自客户端的二进制数据流。

## 使用 JSP 读取表单数据

JSP 以自动解析的方式处理表单数据，根据情况不同使用以下不同的方法：

- **getParameter()：** 调用 request.getParameter() 方法得到一种形式参数的值。

- **getParameterValues()：**如果参数出现不止一次，那么就调用这个方法并返回多个值，例如复选框。

- **getParameterNames()：**如果你想要在当前请求下得到一个所有参数的完整的列表，那么调用这个方法。

- **getInputStream()：** 调用这个方法读取来自客户端二进制数据流。

## 使用 URL 的 GET 方法示例

这是一个简单的 URL 示例，使用 GET 方法将两个值传递给 HelloForm 程序。

**http: // localhost:8080 / main.jsp ? first_name = ZARA&last_name =ALI** 
下面是 **main.jsp** JSP程序来处理由web浏览器给定的输入。我们将使用 **getParameter()** 方法使访问传递信息变得容易：

<pre class="prettyprint notranslate tryit">
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Using GET Method to Read Form Data&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;Using GET Method to Read Form Data&lt;/h1&gt;
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


现在在你的浏览位置框中键入 *http://localhost:8080/main.jsp?first_name=ZARA&last_name=ALI*。这将产生如下所示的结果：

<table cellpadding="5" class="table table-bordered">
<tr><td bgcolor="#f0f0f0">
<h1>Using GET Method to Read Form Data</h1>
<ul class="list">
  <li><p><b>First Name</b>: ZARA</p></li>
  <li><p><b>Last Name</b>: ALI</p></li>
</ul>
</td></tr>
</table>


## 使用表单的 GET 方法的示例

这是一个简单的例子，使用HTML表单和提交按钮传递两个值。我们将使用相同的 JSP  main.jsp 来处理这个输入。

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


将这个 HTML 保存在 hello.htm 文件中，并把它放在 < Tomcat-installation-directory > / webapps /ROOT 目录下。当你访问 *http:/ / localhost:8080 /hello.htm* 时，这就是在表单上面的实际输出。

<form action="javascript:void();" method="get" target="_blank">
First Name: <input type="text" name="first_name" />  <br />
 
Last Name: <input type="text" name="last_name" />
<input type="button" value="Submit" />
</form>

尝试输入姓和名，然后单击提交按钮来查看 tomcat 运行的本地机器上的结果。基于提供的输入，它会产生与上面提到的例子中相似的结果。

## 使用表单的 POST 方法的示例

让我们在上面的 JSP 中做一些小修改来处理 GET 和 POST 方法。下面是main.jsp JSP 程序使用 GET 或 POST 方法来处理 web 浏览器给定的输入。

事实上上面的 JSP 没有改变，因为只有传递参数的方法改变了，并且没有二进制数据被传递到 JSP 程序。文件处理相关的概念将在单独的一章中解释，在这里我们需要读取二进制数据流。

<pre class="prettyprint notranslate">
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Using GET and POST Method to Read Form Data&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;Using GET Method to Read Form Data&lt;/h1&gt;
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


以下是 hello.htm 文件中的内容：

<pre class="prettyprint notranslate">
&lt;html&gt;
&lt;body&gt;
&lt;form action="main.jsp" method="POST"&gt;
First Name: &lt;input type="text" name="first_name"&gt;
&lt;br /&gt;
Last Name: &lt;input type="text" name="last_name" /&gt;
&lt;input type="submit" value="Submit" /&gt;
&lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在让我们把 main.jsp 和 hello.htm  保存到 < Tomcat-installation-directory > / webapps /ROOT 目录下。当你访问 http:/ / localhost:8080 /hello.htm 时，下面是表单的实际输出。

<form action="javascript:void();" method="get" target="_blank">
First Name: <input type="text" name="first_name" />  <br />
 
Last Name: <input type="text" name="last_name" />
<input type="button" value="Submit" />
</form> 
尝试输入姓名，然后单击提交按钮来查看 tomcat 运行的本地机器上的结果。

基于提供的输入，它会产生与上面提到的例子中类似的结果。

## 将复选框数据传递给 JSP 程序

当需要选择多个选项时，就使用复选框。

这是HTML 代码的示例，CheckBox.htm，一个表单中有两个复选框

<pre class="prettyprint notranslate">
&lt;html&gt;
&lt;body&gt;
&lt;form action="main.jsp" method="POST" target="_blank"&gt;
&lt;input type="checkbox" name="maths" checked="checked" /&gt; Maths
&lt;input type="checkbox" name="physics"  /&gt; Physics
&lt;input type="checkbox" name="chemistry" checked="checked" /&gt; 
                                                Chemistry
&lt;input type="submit" value="Select Subject" /&gt;
&lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


上述代码的结果如下所示：

<form action="javascript:void();" method="get" target="_blank">
<input type="checkbox" name="maths" checked="checked" /> Maths
<input type="checkbox" name="physics" /> Physics
<input type="checkbox" name="chemistry" checked="checked" /> Chemistry
<input type="button" value="Select Subject" />
</form> 
以下是 main.jsp JSP 程序为复选框处理由浏览器给定的输入。

<pre class="prettyprint notranslate">
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Reading Checkbox Data&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;Reading Checkbox Data&lt;/h1&gt;
&lt;ul&gt;
&lt;li&gt;&lt;p&gt;&lt;b&gt;Maths Flag:&lt;/b&gt;
   &lt;%= request.getParameter("maths")%&gt;
&lt;/p&gt;&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;b&gt;Physics Flag:&lt;/b&gt;
   &lt;%= request.getParameter("physics")%&gt;
&lt;/p&gt;&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;b&gt;Chemistry Flag:&lt;/b&gt;
   &lt;%= request.getParameter("chemistry")%&gt;
&lt;/p&gt;&lt;/li&gt;
&lt;/ul&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


以上的例子将会产生以下的结果：

<pre class="result notranslate">
<h1>Reading Checkbox Data</h1>
<ul class="list">
  <li><p><b>Maths Flag : </b>: on</p></li>
  <li><p><b>Physics Flag: </b>: null</p></li>
  <li><p><b>Chemistry Flag: </b>: on</p></li>
</ul>
</pre>


## 读取全部表单参数

以下是使用 HttpServletRequest 的 getParameterNames() 方法读取所有可用的表单参数的通用的例子。该方法返回一个枚举，包含一个未指定序列的参数名称。

一旦我们得到一个枚举，我们可以以标准的方式循环这个枚举，使用 *hasMoreElements()*方法来确定何时停止循环，使用 *nextElement() 方法得到每个参数的名字。

<pre class="prettyprint notranslate">
&lt;%@ page import="java.io.*,java.util.*" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;HTTP Header Request Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h2&gt;HTTP Header Request Example&lt;/h2&gt;
&lt;table width="100%" border="1" align="center"&gt;
&lt;tr bgcolor="#949494"&gt;
&lt;th&gt;Param Name&lt;/th&gt;&lt;th&gt;Param Value(s)&lt;/th&gt;
&lt;/tr&gt;
&lt;%
   Enumeration paramNames = request.getParameterNames();

   while(paramNames.hasMoreElements()) {
      String paramName = (String)paramNames.nextElement();
      out.print("&lt;tr&gt;&lt;td&gt;" + paramName + "&lt;/td&gt;\n");
      String paramValue = request.getHeader(paramName);
      out.println("&lt;td&gt; " + paramValue + "&lt;/td&gt;&lt;/tr&gt;\n");
   }
%&gt;
&lt;/table&gt;
&lt;/center&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


以下是hello.htm 中的内容：

<pre class="prettyprint notranslate">
&lt;html&gt;
&lt;body&gt;
&lt;form action="main.jsp" method="POST" target="_blank"&gt;
&lt;input type="checkbox" name="maths" checked="checked" /&gt; Maths
&lt;input type="checkbox" name="physics"  /&gt; Physics
&lt;input type="checkbox" name="chemistry" checked="checked" /&gt; Chem
&lt;input type="submit" value="Select Subject" /&gt;
&lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在试着使用上述 hello.htm 调用JSP，这将生成一个基于给定的输入的结果，类似情况如
下所示：

## 读取全部表单参数

<table width="100%" border="1" align="center" class="table table-bordered">
<tr bgcolor="#949494">
<th>参数名称</th><th>参数值</th>
</tr>
<tr><td>maths</td>
<td>on</td>
</tr>
<tr><td>chemistry</td>
<td>on</td>
</tr>
</table>

你可以试着用上述 JSP 读取其他任何有其他对象的表单数据，如文本框，单选按钮或下拉框等。
