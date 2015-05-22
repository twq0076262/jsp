# JSP - 指令

JSP 指令为容器提供方向和指导，告诉它如何处理 JSP 过程的某些方面。

JSP 指令影响 servlet 类的总体结构。它通常具有以下形式：

``` 
<%@ directive attribute="value" %>
```

指令有若干个属性，你可以以键-值对的形式列出并由逗号分隔。

@ 符号和指令名称之间的空格，以及最后一个属性和结束标志 %> 之间的空格，是可选的。

指令标签有三种类型：

<table class="table table-bordered">
<tr><th style="width:30%">指令 </th><th>描述 </th></tr>
<tr><td>&lt;%@ page ... %&gt;</td><td>定义 page-dependent 属性，比如脚本语言，错误页面和缓冲要求。</td></tr>
<tr><td>&lt;%@ include ... %&gt;</td><td>包含在转换阶段的文件。</td></tr>
<tr><td>&lt;%@ taglib ... %&gt;</td><td>声明了一个用于页面中的标签库，包括自定义操作。 </td></tr>
</table>  

## 页面指令

**页面**指令用于为属于当前 JSP 页面的容器提供指示。你可以在 JSP 页面的任何地方编写页面指令代码。按照惯例，通常在 JSP 页面的顶部编写页面指令代码。

下面是页面指令的基本语法：

``` 
<%@ page attribute="value" %>
```

你可以编写等同于上述语法的 XML，如下所示：

``` 
<jsp:directive.page attribute="value" />
```

## 属性

以下是页面指令相关的属性列表：

<table class="table table-bordered">
<tr><th style="width:30%">属性 </th><th>目的 </th></tr>
<tr><td>buffer</td><td>指定一个输出流的缓冲模型。</td></tr>
<tr><td>autoFlush</td><td>控制 servlet 输出缓冲区的行为。</td></tr>
<tr><td>contentType</td><td>定义了字符编码方案。</td></tr>
<tr><td>errorPage</td><td>定义了 Java 未检查运行时异常报告的另一个 JSP 的 URL。</td></tr>
<tr><td>isErrorPage</td><td>表明这个 JSP 页面是否是由另一个 JSP 页面的 errorPage 属性指定的 URL。</td></tr>
<tr><td>extends</td><td>指定一个超类，生成的 servlet 必须扩展</td></tr>
<tr><td>import</td><td>指定在 JSP 中使用的包或类的列表，正如 Java 导入声明为 Java 类所做的相同。</td></tr>
<tr><td>info</td><td>定义一个字符串，可以访问 servlet 的 getServletInfo()方法。</td></tr>
<tr><td>isThreadSafe</td><td>为生成的 servlet 定义线程模型。</td></tr>
<tr><td>language</td><td>定义了在 JSP 页面中使用的编程语言。</td></tr>
<tr><td>session</td><td>指定 JSP 页面是否参与 HTTP 会话</td></tr>
<tr><td>isELIgnored</td><td>指定 JSP 页面中的 EL 表达式中是否将被忽略。</td></tr>
<tr><td>isScriptingEnabled</td><td>决定是否允许使用脚本元素。</td></tr>
</table>  

关于上述属性更详细的描述，请看 [**Page Directive**](page-directive.md)

## 包含指令

**包含**指令用于在转换阶段包含一个文件。这个指令告诉容器在转换阶段将其他外部文件的内容与当前 JSP 合并。你可以在你的 JSP 页面中的任何位置编写 *include* 指令。

一般使用这个指令的形式如下：

``` 
<%@ include file="relative url" >
```

包含指令中的文件名实际上是一个相对 URL。如果你只指定一个文件名而没有相关路径，JSP 编译器就会假定文件与你的 JSP 在同一个目录下。

你可以编写等同于上述语法的 XML，如下所示：

``` 
<jsp:directive.include file="relative url" />
```

关于包含指令的更详细的描述，请看 [**Include Directive**](include-directive.md)

## taglib 指令

JSP API 允许用户定义自定义的 JSP 标签，看起来像 HTML 或 XML 标签，且标签库是一组用户定义的标签，能够实现自定义的行为。

**taglib** 指令声明了 JSP 页面使用一组自定义标签，识别库的位置，并提供方法来确定 JSP 页面中的自定义标签。

taglib 指令遵循以下语法：

``` 
<%@ taglib uri="uri" prefix="prefixOfTag" >
```

其中，**uri** 属性值解析为容器理解的一个位置，**prefix** 属性通知容器什么标记是自定义操作。

你可以编写相当于上述的语法的 XML，如下所示：

``` 
<jsp:directive.taglib uri="uri" prefix="prefixOfTag" />
```

关于 taglib 指令的更详细的描述，请看 [**Taglib Directive**](taglib-directive.md)


