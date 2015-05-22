# JSP - 操作

JSP 操作使用 XML 语法结构来控制 servlet 引擎的行为。你可以动态地插入一个文件，重组 JavaBean 组件，将用户转换到另一个页面，或为 Java 插件生成 HTML。

操作元素只有一个语法，因为它符合 XML 标准：

``` 
<jsp:action_name attribute="value" />
```

动作元素基本上是预定义的函数，有以下 JSP 操作：

<table class="table table-bordered">
<tr><th style="width:30%">语法</th><th>目的</th></tr>
<tr><td>jsp:include</td><td>当请求页面时，包含一个文件</td></tr>
<tr><td>jsp:useBean</td><td>发现或实例化一个 JavaBean </td></tr>
<tr><td>jsp:setProperty</td><td> JavaBean 的属性集</td></tr>
<tr><td>jsp:getProperty</td><td>将 JavaBean 的属性嵌入到输出中</td></tr>
<tr><td>jsp:forward</td><td>将请求转发给一个新页面</td></tr>
<tr><td>jsp:plugin</td><td>生成浏览器-特定代码，为 Java 插件创建 OBJECT 或 EMBED 标签</td></tr>
<tr><td>jsp:element</td><td>动态的定义 XML 元素</td></tr>
<tr><td>jsp:attribute</td><td>定义了动态定义的 XML 元素的属性</td></tr>
<tr><td>jsp:body</td><td>定义了动态定义 XML 元素的 body </td></tr>
<tr><td>jsp:text</td><td>用于在 JSP 页面和文档中编写模板</td></tr>
</table>

## 共同的属性

对于所有的操作元素来说，有两个属性是共同的：**id** 属性和 **scope** 属性。

- **Id 属性：** Id 属性惟一地标识操作元素，并允许在 JSP 页面内引用操作。如果操作创建了一个对象的一个实例，那么 id 值可以通过隐式对象 PageContext 来引用该操作

- **Scope属性：** 这个属性标识了操作元素的生命周期。id 属性和 scope 属性是直接相关的，因为 scope 属性决定了 id 属性相关的对象的生命周期。scope 属性有四个可能值：(a)页面，(b)请求，(c)会话和(d)应用程序。

## `<jsp:include>`操作

此操作允许你将文件插入到将要生成的页面中。语法如下：

``` 
<jsp:include page="relative URL" flush="true" />
```

该操作与包含指令不同，包含指令在 JSP 页面转换成 servlet 时插入文件，该操作在请求页面时插入文件。

下面是与包含操作相关的属性列表：

<table class="table table-bordered">
<tr><th style="width:30%">属性 </th><th>描述 </th></tr>
<tr><td>page</td><td>要被包含的页面的相对 URL。 </td></tr>
<tr><td>flush</td><td>布尔属性决定了包含的资源在被包含之前其缓冲区是否刷新。</td></tr>
</table> 

## 例子

让我们定义以下两个文件(a)date.jsp 和(b)main.jsp，如下:

以下是 date.jsp 文件的内容：
 
<pre class="prettyprint notranslate">
&lt;p&gt;
   Today's date: &lt;%= (new java.util.Date()).toLocaleString()%&gt;
&lt;/p&gt;
</pre>

以下是 main.jsp 文件的内容：

<pre class="prettyprint notranslate tryit">
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;The include Action Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h2&gt;The include action Example&lt;/h2&gt;
&lt;jsp:include page="date.jsp" flush="true" /&gt;
&lt;/center&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在让我们把所有这些文件保存在在根目录中，并试图访问 main.jsp。这将显示如下所示结果：

 <pre class="result notranslate">
<center>
<h2>The include action Example</h2>
   Today's date: 12-Sep-2010 14:54:22
</center>
</pre>



## `<jsp:useBean>` 操作

**useBean** 操作具有多种用途。它首先利用 id 和 scope 变量搜索现有对象。如果没有找到一个对象，那么它会试图创建指定的对象。

加载 bean 的最简单的方式如下：

``` 
<jsp:useBean id="name" class="package.class" />
```

加载 bean 类完成后，你可以使用 **jsp:setProperty** 和 **jsp:getProperty** 操作来修改和检索 bean 属性。

下面是与 useBean 操作关联的属性列表：

<table class="table table-bordered">
<tr><th style="width:30%">属性 </th><th>描述 </th></tr>
<tr><td>class</td><td>指定 bean 的全部包名。</td></tr>
<tr><td>type</td><td>指定将在对象中引用的变量的类型。</td></tr>
<tr><td>beanName</td><td>通过 java.beans.Beans 类中的 instantiate()方法给定 bean 名称。</td></tr>
</table>  

在给出与这些操作有关的有效的例子之前，让我们先讨论一下 **jsp:setProperty** 和 **jsp:getProperty** 操作。

## `<jsp:setProperty>` 操作

**setProperty** 操作设置了 Bean 的属性。在定义该操作之前， Bean 一定已经预定义了。有两种使用 setProperty 操作的基本的方式：

你可以使用 jsp:setProperty 之后，但是在该操作外面，使用一个 jsp:useBean 元素，如下所示：

``` 
<jsp:useBean id="myName" ... />
...
<jsp:setProperty name="myName" property="someProperty" .../>
```

在这种情况下，无论新的 bean 是否实例化或现有的 bean 是否被发现，jsp:setProperty 都会被执行。

jsp:setProperty 可以出现的第二个背景是在 jsp:useBean 元素内部，如下所示：

``` 
<jsp:useBean id="myName" ... >
...
   <jsp:setProperty name="myName" property="someProperty" .../>
</jsp:useBean>
```

这里，当且仅当实例化一个新对象时，jsp:setProperty 才会被执行，如果一个现有的对象被发现时，它不会被执行。

下面是与 setProperty 操作相关的属性列表：

<table class="table table-bordered">
<tr><th style="width:30%">属性 </th><th>描述 </th></tr>
<tr><td>name</td><td>指定了将被设置属性的 bean。该 Bean 一定是之前定义的。</td></tr>
<tr><td>property</td><td>表明了你想设置的属性。值为“*”意味着所有请求的名字与 bean 属性名字匹配的参数将被传递给适当的 setter 方法。</td></tr>
<tr><td>value</td><td>值分配给给定属性的值。参数的值为 null 或参数不存在时，setProperty 操作将被忽略。</td></tr>
<tr><td>param</td><td>param 属性是请求参数的名称，该属性会接收该请求参数的值。你不能同时使用值和参数，但是使用其中的一个是允许的。</td></tr>
</table>  

## `<jsp:getProperty>` 操作

**getProperty** 操作用于检索给定属性的值并将它转换成一个字符串，并最终将它插入到输出中。

getProperty 操作只有两个属性，两者都是必需的，其简单的语法如下所示：

``` 
<jsp:useBean id="myName" ... />
...
<jsp:getProperty name="myName" property="someProperty" .../>
```

以下是与 setProperty 操作相关的属性属性列表：

<table class="table table-bordered">
<tr><th style="width:30%">属性 </th><th>描述 </th></tr>
<tr><td>name</td><td>有检索属性的 Bean 的名称。Bean 一定是之前定义的。</td></tr>
<tr><td>property</td><td> property 属性是要被检索的 Bean 属性的名称。</td></tr>
</table> 

## 例子

让我们定义一个测试的 bean，在例子中使用如下所示：

``` 
/* File: TestBean.java */
package action;
public class TestBean {
   private String message = "No message specified";
   public String getMessage() {
      return(message);
   }
   public void setMessage(String message) {
      this.message = message;
   }
}
```

编译以上代码生成 TestBean.class 文件并确保将 TestBean.class 复制在 C:\ apache-tomcat-7.0.2 \ webapps \ web - inf \ classes \action 文件夹中，且类路径变量也应设置为该文件夹：

现在在 main.jsp 文件中使用以下代码，该文件加载 bean 并 set/get 了一个简单的字符串参数：

<pre class="prettyprint notranslate tryit">
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Using JavaBeans in JSP&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h2&gt;Using JavaBeans in JSP&lt;/h2&gt;
 
&lt;jsp:useBean id="test" class="action.TestBean" /&gt;
 
&lt;jsp:setProperty name="test" 
                    property="message" 
                    value="Hello JSP..." /&gt;
 
&lt;p&gt;Got message....&lt;/p&gt;
 
&lt;jsp:getProperty name="test" property="message" /&gt;
 
&lt;/center&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在试着访问 main.jsp，将会出现如下所示的结果：

<pre class="result notranslate">
<center>
<h2>Using JavaBeans in JSP</h2>
Got message....<br />
Hello JSP...
</center>
</pre>


## `<jsp:forward>` 操作

**forward** 操作终止当前页面的操作并将请求转发给另一个资源，如一个静态页面，另一个 JSP 页面，或 Java Servlet。

该操作的简单的语法如下所示：

``` 
<jsp:forward page="Relative URL" />
```

以下是与 forward 操作相关的属性列表：

<table class="table table-bordered">
<tr><th style="width:30%">属性 </th><th>描述 </th></tr>
<tr><td>page</td><td>应该包括另一个资源的相对 URL，比如静态页面，另一个 JSP 页面，或 Java Servlet。</td></tr>
</table>  

## 例子

让我们重用以下两个文件(a)date.jsp (b)main.jsp，如下所示：

以下是 date.jsp 文件的内容：

<pre class="prettyprint notranslate">
&lt;p&gt;
   Today's date: &lt;%= (new java.util.Date()).toLocaleString()%&gt;
&lt;/p&gt;
</pre>


以下是 main.jsp 文件的内容：

<pre class="prettyprint notranslate">
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;The include Action Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h2&gt;The include action Example&lt;/h2&gt;
&lt;jsp:forward page="date.jsp" /&gt;
&lt;/center&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在让我们把所有这些文件保存在在根目录中并试图访问 main.jsp。这将显示类似如下所示的结果。这里丢弃主页的内容，只显示来自转发页面的内容。

<pre class="result notranslate">
<center>
   Today's date: 12-Sep-2010 14:54:22
</center>
</pre>


## `<jsp:plugin>` 操作

**插件**用于将 Java 组件插入到 JSP 页面中。它决定了浏览器的类型以及需要插入的 < object > 或 < embed > 标签的类型。

如果所需的插件不存在，它将下载插件，然后执行 Java 组件。Java 组件可以是一个 Applet 或一个 JavaBean。

插件操作有几个属性，对应常用的生成 Java 组件的 HTML 标签。< param >元素也可以用来给 Applet 或 Bean 发送参数。

下面是使用插件操作的典型的语法：

``` 
<jsp:plugin type="applet" codebase="dirname" code="MyApplet.class"
                           width="60" height="80">
   <jsp:param name="fontcolor" value="red" />
   <jsp:param name="background" value="black" />
   <jsp:fallback>
      Unable to initialize Java Plugin
   </jsp:fallback>
</jsp:plugin>
```

如果你感兴趣的话，你可以使用applet尝试该操作。一个新元素，< fallback >元素，当组件失败时，可以用来指定一个错误字符串发送给用户。

## `<jsp:element>` 操作

## `<jsp:attribute>` 操作

## `<jsp:body>` 操作

< jsp:element >，< jsp:attribute >和< jsp:body >操作是用于动态的定义 XML 元素的。动态这个词是很重要的，因为这意味着 XML 元素可以在请求时生成，而不是在编译时静态生成。

下面是一个简单的例子来动态定义 XML 元素：

<pre class="prettyprint notranslate">
&lt;%@page language="java" contentType="text/html"%&gt;
&lt;html xmlns="http://www.w3c.org/1999/xhtml"
      xmlns:jsp="http://java.sun.com/JSP/Page"&gt;

&lt;head&gt;&lt;title&gt;Generate XML Element&lt;/title&gt;&lt;/head&gt;
&lt;body&gt;
&lt;jsp:element name="xmlElement"&gt;
&lt;jsp:attribute name="xmlElementAttr"&gt;
   Value for the attribute
&lt;/jsp:attribute&gt;
&lt;jsp:body&gt;
   Body for XML element
&lt;/jsp:body&gt;
&lt;/jsp:element&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

在运行时会产生如下所示的 HTML 代码：

<pre class="prettyprint notranslate">
&lt;html xmlns="http://www.w3c.org/1999/xhtml"
      xmlns:jsp="http://java.sun.com/JSP/Page"&gt;
 
&lt;head&gt;&lt;title&gt;Generate XML Element&lt;/title&gt;&lt;/head&gt;
&lt;body&gt;
&lt;xmlElement xmlElementAttr="Value for the attribute"&gt;
   Body for XML element
&lt;/xmlElement&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


## `<jsp:text>` 操作

<jsp:text>操作可以用于在 jsp 页面和文档中编写模板文本。以下是该操作的简单的语法：

``` 
<jsp:text>Template data</jsp:text>
```

该模板内部不能包含其他元素；它只能包含文本和 EL 表达式(注：EL 表达式将在后续章节中解释)。注意，在 XML 文件中，你不能使用如 ${whatever > 0} 的表达式，因为大于号是非法的。相反，使用 gt 形式，如 ${whatever gt 0} 或其他方法在一个 CDATA 区域中嵌入值。

``` 
<jsp:text><![CDATA[<br>]]></jsp:text>
```

如果你需要包含 DOCTYPE 声明，例如对 XHTML 来说，你还必须使用 < jsp:text > 元素，如下所示：

<pre class="prettyprint notranslate">
&lt;jsp:text&gt;&lt;![CDATA[&lt;!DOCTYPE html
PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"DTD/xhtml1-strict.dtd"&gt;]]&gt;
&lt;/jsp:text&gt;
&lt;head&gt;&lt;title&gt;jsp:text action&lt;/title&gt;&lt;/head&gt;
&lt;body&gt;

&lt;books&gt;&lt;book&gt;&lt;jsp:text&gt;  
    Welcome to JSP Programming
&lt;/jsp:text&gt;&lt;/book&gt;&lt;/books&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>


在使用< jsp:text >操作和不使用该操作的两种情况下尝试上述例子。
