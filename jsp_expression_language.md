# 表达式语言（EL） 

JSP 表达式语言(EL)可以方便地访问存储在 javabean 组件中的应用程序的数据。JSP EL 允许创建表达式**(a)**算术和**(b)**逻辑。在一个 JSP EL 表达式中，你可以使用整数、浮点型数字、字符串、内置的布尔常量值为 true 和 false 和 null。 

## 简单的语法： 

通常，当你给 JSP 标签指定一个属性值时，你只需使用一个字符串。例如：

``` 
<jsp:setProperty name="box" property="perimeter" value="100"/>
```

JSP EL 允许你给表达式指定这些属性值。一个简单的 JSP EL 语法如下： 

``` 
${expr}
```

这里的 expr 是指定表达式本身。在 JSP EL 中最常见的操作符是 **.** 和 **[]**。这两个操作符允许访问 Java beans 和内置 JSP 对象的各种属性。 

例如可以用一个表达式编写上面的语法 < jsp:setProperty >标签，如下：

``` 
<jsp:setProperty name="box" property="perimeter" 
                 value="${2*box.width+2*box.height}"/>
```

当 JSP 编译器在一个属性中看到了 $ { } 形式，它可以生成计算表达式的代码，并且替换表达式的值。 

你还可以在模板文本中对一个标签使用 JSP EL 表达式。例如，把 < jsp:text > 标签简单的插入到一个 JSP 的主体内容中。在下面的 < jsp:文本> 声明中，插入 < h1>Hello JSP!< /h1> 到 JSP 输出：

<pre class="prettyprint notranslate"> 
&lt;jsp:text&gt;
&lt;h1&gt;Hello JSP!&lt;/h1&gt;
&lt;/jsp:text&gt;
</pre>


你可以在< jsp:text> 标签(或任何其他标签)的标签体内引入一个 JSP EL 表达式，对属性使用 $ { } 语法。例如：

``` 
<jsp:text>
Box Perimeter is: ${2*box.width + 2*box.height}
</jsp:text>
```

EL 表达式可以使用括号组成子表达式。例如，$ {(1 + 2)* 3 } = 9，但 $ { 1 +(2 * 3)} = 7。

禁止 EL 表达式的计算，我们指定页面指令的 isELIgnored 属性如下：

``` 
<%@ page isELIgnored ="true|false" %>
```
 
这个属性的有效值是 true 和 false。如果它是 true，当它们出现在静态文本或标签属性时，EL 表达式被忽略。如果它是 false，EL 表达式都由容器进行计算。 

## EL 的基本操作： 

JSP 表达式语言(EL)支持大多数 Java 支持的算术和逻辑运算符。下面是最常用的操作符的列表：

<table class="table table-bordered">
<tr><th style="width:30%">操作	</th><th>描述 </th></tr>
<tr><td>. </td><td>访问bean属性或映射项</tr></td>
<tr><td>[]</td><td> 访问数组或链表元素</tr></td>
<tr><td>( )</td><td> 组成子表达式来修改计算顺序</tr></td>
<tr><td>+ </td><td>加</tr></td>
<tr><td>-</td><td> 减或负数</tr></td>
<tr><td>*</td><td> 乘</tr></td>
<tr><td>/ or div</td><td> 除</tr></td>
<tr><td>% or mod</td><td> 模计算/余数</tr></td>
<tr><td>== or eq</td><td> 等于</tr></td>
<tr><td>!= or ne</td><td> 不等于</tr></td>
<tr><td>&lt; or lt </td><td>小于</tr></td>
<tr><td>&gt; or gt</td><td> 大于</tr></td>
<tr><td>&lt;= or le </td><td>小于等于</tr></td>
<tr><td>&gt;= or gt </td><td>大于等于</tr></td>
<tr><td>&amp;&amp; or and </td><td>逻辑与</tr></td>
<tr><td>|| or or</td><td> 逻辑或</tr></td>
<tr><td>! or not</td><td> 一元布尔补集</tr></td>
<tr><td>empty </td><td>空的变量值</tr></td>
</table>
	
## JSP EL 中的函数： 

JSP EL 同样允许使用函数表达式。这些功能必须定义在自定义标签库中。一个函数利用下面的语法使用：

``` 
${ns:func(param1, param2, ...)}
```

其中，ns 是函数的命名空间，func 是函数名，param1 是第一个参数值。例如，函数 fn:length，它是 JSTL 库的一部分，可以使用它得到一个字符串的长度，如下所示。

``` 
${fn:length("Get my length")}
```

要从(标准或自定义)标签库中使用一个函数，你必须在你的服务器上安装库，而且必须在 JSP 中使用 < taglib > 指令来引用该库，这个在 JSTL 章有解释。 

## JSP EL 隐式对象： 

JSP 表达式语言支持以下隐式对象： 

<table class="table table-bordered">
<tr><th style="width:30%">隐式对象	</th><th>描述 </th></tr>
<tr><td>pageScope</td><td>变量范围是页面范围</td></tr>
<tr><td>requestScope</td><td>变量范围是请求范围</td></tr>
<tr><td>sessionScope</td><td>变量范围是会话范围</td></tr>
<tr><td>applicationScope</td><td>变量范围是应用范围</td></tr>
<tr><td>param</td><td>请求参数作为字符串</td></tr>
<tr><td>paramValues</td><td>请求参数作为字符串集合</td></tr>
<tr><td>header</td><td>HTTP请求标头作为字符串</td></tr>
<tr><td>headerValues</td><td>HTTP请求标头作为字符串集合</td></tr>
<tr><td>initParam</td><td>上下文初始化参数</td></tr>
<tr><td>cookie</td><td>Cookie 值</td></tr>
<tr><td>pageContext</td><td>当前页面的 JSP PageContext 对象</td></tr>
</table>

你可以在表达式中使用这些对象，把它们看做是变量。这里有一些明确概念的例子：

## pageContext 对象： 

pageContext 对象允许你访问 pageContext JSP 对象。通过 pageContext 对象，你可以访问请求对象。例如，要访问请求传入的查询字符串，你可以使用下面的表达式：

``` 
${pageContext.request.queryString}
```

## Scope 对象： 

sessionScope、pageScope、requestScop、applicationScope 变量在每个级别范围提供变量存储。 

例如，如果你需要显式地在应用范围内访问 box 变量，你可以通过 applicationScope 变量作为 applicationScope.box 来访问。 

## param 和 paramValues 对象： 

param 和 paramValues 对象通常通过 request.getParameter 和 request.getParameterValues 方法来有效的访问参数值。 

例如，使用表达式 ${param.order} 或 ${param["order"]} 来访问命名为 order 的参数。 

下面是访问命名为 username 的请求参数的例子：


<pre class="prettyprint notranslate"> 
&lt;%@ page import="java.io.*,java.util.*" %&gt;
&lt;%
    String title = "Accessing Request Param";
%&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;% out.print(title); %&gt;&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;&lt;% out.print(title); %&gt;&lt;/h1&gt;
&lt;/center&gt;
&lt;div align="center"&gt;
&lt;p&gt;${param["username"]}&lt;/p&gt;
&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

param 对象返回单个字符串值，而 paramValues 对象返回字符串数组。

## header 和 headerValues 对象： 

header 和 headerValue 对象通常通过 request.getHeader 和 request.getHeaders 方法来有效的访问标头值。 

例如，使用表达式 ${header.user-agent} 或 ${header["user-agent"]} 来访问命名得 user-agent 的标头。 

下面是访问命名为 user-agent 的标头参数的例子：

<pre class="prettyprint notranslate"> 
&lt;%@ page import="java.io.*,java.util.*" %&gt;
&lt;%
    String title = "User Agent Example";
%&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;% out.print(title); %&gt;&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;&lt;% out.print(title); %&gt;&lt;/h1&gt;
&lt;/center&gt;
&lt;div align="center"&gt;
&lt;p&gt;${header["user-agent"]}&lt;/p&gt;
&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


显示的结果如下：

<pre class="result notranslate">
<h1>User Agent Example</h1>
<div align="center">
<p>Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1; WOW64; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; HPNTDF; .NET4.0C; InfoPath.2)</p>
</div>
</pre>


header 对象返回单个字符串值，而 headerValues 对象返回字符串数组。
