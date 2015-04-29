# 标准标签库（JSTL）教程 

JSP 标准标签库（JSTL）是一组有效的 JSP 标签，它封装了很多 JSP 应用程序的核心功能。 

JSTL 支持普通、结构任务，如迭代和条件，操作 XML 文件标签，国际化标签，和 SQL 标签。它也提供了一个整合现有 JSTL 标签和自定义标签的框架。 

JSTL 标签根据它们的功能进行分类，划分到 JSTL 标签库中，当创建一个 JSP 页面时，可以使用这些标签： 

- 核心标签库

- 格式标签库

- SQL 标签库

- XML 标签库

- JSTL 函数标签库 

## 安装 JSTL 标签库： 

如果你使用的是 Apache Tomcat 容器，然后遵循以下两个简单的步骤： 

- 从 Apache Standard Taglib，下载二进制分布，打开压缩文件。

- 为了从 Jakarta Taglibs 分布中使用标准标签库，简单的复制分布库目录中的 JAR 文件到你的应用程序的 webapps\ROOT\WEB-INF\lib 目录中。 

为了使用所有的库，你必须在要使用该库的每个 JSP 页面的头部中引入<taglib>指令。 

## 核心标签库： 

核心标签库是被广泛使用的 JSTL 标签库。下面是在 JSP 页面中引入核心标签库时需要使用的指令：

``` 
<%@ taglib prefix="c" 
           uri="http://java.sun.com/jsp/jstl/core" %>
```

接下来的是核心标签库的标签： 

<table class="table table-bordered">
<tr><th style="width:30%">标签</th><th>描述 </th></tr>
<tr><td><a href="/jsp/jstl_core_out_tag.htm">&lt;c:out &gt;</a></td><td>类似于 java 表达式<%= ... >，但是表达式。 </td></tr>
<tr><td><a href="/jsp/jstl_core_set_tag.htm">&lt;c:set &gt;</a></td><td>在某个范围内设置表达式的值。</td></tr>
<tr><td><a href="/jsp/jstl_core_remove_tag.htm">&lt;c:remove &gt;</a></td><td>删除一个域变量（从一个特殊的被指定的范围）。 </td></tr>
<tr><td><a href="/jsp/jstl_core_catch_tag.htm">&lt;c:catch&gt;</a></td><td>抛出任何发生在它的主体中的异常，并且有选择的公开它。</td></tr>
<tr><td><a href="/jsp/jstl_core_if_tag.htm">&lt;c:if&gt;</a></td><td>简单的条件标签，如果提供的条件是 true，则执行标签体的内容。</td></tr>
<tr><td><a href="/jsp/jstl_core_choose_tag.htm">&lt;c:choose&gt;</a></td><td>简单的条件标签，用标签< when>和< otherwise>建立一个互斥条件操作的上下文。 </td></tr>
<tr><td><a href="/jsp/jstl_core_choose_tag.htm">&lt;c:when&gt;</a></td><td>< choose>的子标签，如果它的条件为“true”，则运行标签体的内容。</td></tr>
<tr><td><a href="/jsp/jstl_core_choose_tag.htm">&lt;c:otherwise &gt;</a></td><td><choose>的子标签，它出现在< when>标签之后，只有当先前的条件结果为“false”运行它。</td></tr>
<tr><td><a href="/jsp/jstl_core_import_tag.htm">&lt;c:import&gt;</a></td><td>检索绝对或相对的 URL 并且显示它的内容到其他的页面，在“var”中的一个 String 类型，或者在“varReader”中的一个 Reader 类型。</td></tr>
<tr><td><a href="/jsp/jstl_core_foreach_tag.htm">&lt;c:forEach &gt;</a></td><td>基本的迭代标签，接受多种不同的集合类型，支持子集和其他的功能。</td></tr>
<tr><td><a href="/jsp/jstl_core_foreach_tag.htm">&lt;c:forTokens&gt;</a></td><td>迭代使用分隔符，分隔提供的定界符。</td></tr>
<tr><td><a href="/jsp/jstl_core_param_tag.htm">&lt;c:param&gt;</a></td><td>添加一个参数到包含“import”标签的 URL。</td></tr>
<tr><td><a href="/jsp/jstl_core_redirect_tag.htm">&lt;c:redirect &gt;</a></td><td>重新定向到的一个新的 URL。</td></tr>
<tr><td><a href="/jsp/jstl_core_url_tag.htm">&lt;c:url&gt;</a></td><td>创建一个带有选项查询参数的 URL。</td></tr>
</table>

## 格式标签库： 

JSTL 的格式标签库是用于格式化和显示国际化网址的文本、日期、时间和数字。下面是在 JSP 页面中引入格式标签库时需要使用的指令： 

``` 
<%@ taglib prefix="fmt" 
           uri="http://java.sun.com/jsp/jstl/fmt" %>
```

接下来的是格式标签库的标签： 

<table class="table table-bordered">
<tr><th style="width:30%">标签</th><th>描述 </th></tr>
<tr><td><a href="/jsp/jstl_format_formatnumber_tag.htm">&lt;fmt:formatNumber&gt;</a></td><td>用特定的精度或格式呈现数值。</td></tr>
<tr><td><a href="/jsp/jstl_format_parsenumber_tag.htm">&lt;fmt:parseNumber&gt;</a></td><td>将一个表示数值、货币或百分比格式化字符串解析成数值对象。</td></tr>
<tr><td><a href="/jsp/jstl_format_formatdate_tag.htm">&lt;fmt:formatDate&gt;</a></td><td>将日期和/或时间对象格式化成指定的风格和模式</td></tr>
<tr><td><a href="/jsp/jstl_format_parsedate_tag.htm">&lt;fmt:parseDate&gt;</a></td><td>将用字符串表示的日期和/或时间解析成日期对象。</td></tr>
<tr><td><a href="/jsp/jstl_format_bundle_tag.htm">&lt;fmt:bundle&gt;</a></td><td>使用它的标签体来加载一个资源包。</td></tr>
<tr><td><a href="/jsp/jstl_format_setlocale_tag.htm">&lt;fmt:setLocale&gt;</a></td><td>在区域配置变量中存储指定的区域。</td></tr>
<tr><td><a href="/jsp/jstl_format_setbundle_tag.htm">&lt;fmt:setBundle&gt;</a></td><td>加载一个资源包并且将其存储在指定作用域或者资源包配置变量中。</td></tr>
<tr><td><a href="/jsp/jstl_format_timezone_tag.htm">&lt;fmt:timeZone&gt;</a></td><td>在标签体的内容中，对指定的时区进行时间格式化和解析操作。</td></tr>
<tr><td><a href="/jsp/jstl_format_settimezone_tag.htm">&lt;fmt:setTimeZone&gt;</a></td><td>将指定的时区存储在时区配置变量中。</td></tr>
<tr><td><a href="/jsp/jstl_format_message_tag.htm">&lt;fmt:message&gt;</a></td><td>显示国际化的信息。</td></tr>
<tr><td><a href="/jsp/jstl_format_requestencoding_tag.htm">&lt;fmt:requestEncoding&gt;</a></td><td>设置请求中字符的编码格式。</td></tr>
</table>

## SQL 标签库： 

JSTL 的 SQL 标签库提供了标签给交互的关系数据库(RDBMSs)如 Oracle、mySQL 或 Microsoft SQL Server。 

下面是在 JSP 页面中引入格式标签库时需要使用的指令：

```  
<%@ taglib prefix="sql" 
           uri="http://java.sun.com/jsp/jstl/sql" %>
```

接下来的是格式标签库的标签： 

<table class="table table-bordered">
<tr><th style="width:30%">标签</th><th>描述 </th></tr>
<tr><td><a href="/jsp/jstl_sql_setdatasource_tag.htm">&lt;sql:setDataSource&gt;</a></td><td>创建一个简单的只适合原型的数据源。</td></tr>
<tr><td><a href="/jsp/jstl_sql_query_tag.htm">&lt;sql:query&gt;</a></td><td>在它的标签体中或通过 SQL 属性，执行定义的 SQL 查询操作。</td></tr>
<tr><td><a href="/jsp/jstl_sql_update_tag.htm">&lt;sql:update&gt;</a></td><td>在它的标签体中或通过 SQL 属性，执行定义的 SQL 更新操作。</td></tr>
<tr><td><a href="/jsp/jstl_sql_param_tag.htm">&lt;sql:param&gt;</a></td><td>将 SQL 语句中的一个参数设置为指定的值。</td></tr>
<tr><td><a href="/jsp/jstl_sql_dateparam_tag.htm">&lt;sql:dateParam&gt;</a></td><td>将 SQL 语句中的一个参数设置为指定的 java.util.Date 值。</td></tr>
<tr><td><a href="/jsp/jstl_sql_transaction_tag.htm">&lt;sql:transaction &gt;</a></td><td>为嵌套数据库操作元素提供了一个共享连接，建立执行所有语句组成一个事务。</td></tr>
</table>

## XML 标签库： 

JSTL 的 XML 标签库提供了创建和操纵 XML 文档的 JSP-centric 方式。下面是在 JSP 页面中引入 XML 标签库时需要使用的指令： 

对于交互的 XML 数据，JSTL 的 XML 标签库有自定义标签。它包括解析 XML、转换XML 数据和基于 XPath 语言表达式的流程控制。

``` 
<%@ taglib prefix="x" 
           uri="http://java.sun.com/jsp/jstl/xml" %>
``` 

在你处理这个例子之前，你应该需要复制以下两个 XML 和 XPath 相关的库到你的 <Tomcat Installation Directory>\lib 中： 

- **XercesImpl.jar:** 从 [http://www.apache.org/dist/xerces/j/](http://www.apache.org/dist/xerces/j/) 下载

- **xalan.jar:** 从 [http://xml.apache.org/xalan-j/index.html](http://xml.apache.org/xalan-j/index.html) 下载 

接下来的是格式标签库的标签： 

<table class="table table-bordered">
<p>Following is the list of XML JSTL Tags:</p>
<tr><th style="width:30%">标签</th><th>描述 </th></tr>
<tr><td><a href="/jsp/jstl_xml_out_tag.htm">&lt;x:out&gt;</a></td><td>类似于 java 表达式 <%= ... >，但是 XPath 表达式。</td></tr>
<tr><td><a href="/jsp/jstl_xml_parse_tag.htm">&lt;x:parse&gt;</a></td><td>要么通过属性要么在标签体中，用于解析特定的XML数据。</td></tr>
<tr><td><a href="/jsp/jstl_xml_set_tag.htm">&lt;x:set &gt;</a></td><td>设置 XPath 表达式的变量值。</td></tr>
<tr><td><a href="/jsp/jstl_xml_if_tag.htm">&lt;x:if &gt;</a></td><td>计算测试的XPath表达式，如果它是 true，就执行它的标签体中的内容。如果测试条件是 false，忽略这个标签体中内容。</td></tr>
<tr><td><a href="/jsp/jstl_xml_foreach_tag.htm">&lt;x:forEach&gt;</a></td><td>在 XML 文件中循环顶点。</td></tr>
<tr><td><a href="/jsp/jstl_xml_choose_tag.htm">&lt;x:choose&gt;</a></td><td>简单的条件标签，用标签< when>和< otherwise>建立一个互斥条件操作的上下文。</td></tr>
<tr><td><a href="/jsp/jstl_xml_choose_tag.htm">&lt;x:when &gt;</a></td><td>< choose>的子标签，如果它的条件为“true”，则运行标签体的内容。</td></tr>
<tr><td><a href="/jsp/jstl_xml_choose_tag.htm">&lt;x:otherwise &gt;</a></td><td>< choose>的子标签，它出现在< when>标签之后，只有当先前的条件结果为“false”运行它。</td></tr>
<tr><td><a href="/jsp/jstl_xml_transform_tag.htm">&lt;x:transform &gt;</a></td><td>应用一个 XSL 转换到一个 XML 文件中。</td></tr>
<tr><td><a href="/jsp/jstl_xml_param_tag.htm">&lt;x:param &gt;</a></td><td>在 XSLT 样式表中使用转换标签设置参数。</td></tr>
</table>
 
## JSTL 函数标签库： 

JSTL 函数标签库包含了大量的标准函数，其中大多数都是御用字符串处理的函数。下面是在 JSP 页面中引入 JSTL 函数标签库时需要使用的指令：

``` 
<%@ taglib prefix="fn" 
           uri="http://java.sun.com/jsp/jstl/functions" %>
```

接下来的是 JSTL 函数标签库的标签： 

<table class="table table-bordered">
<tr><th style="width:33%">函数</th><th>描述 </th></tr>
<tr><td><a href="/jsp/jstl_function_contains.htm">fn:contains()</a></td><td>判断输入的字符串是否包含指定的子字符串。 </td></tr>
<tr><td><a href="/jsp/jstl_function_containsignorecase.htm">fn:containsIgnoreCase()</a></td><td>判断输入的字符串是否包含指定的子字符串，判断时忽略大小写。</td></tr>
<tr><td><a href="/jsp/jstl_function_endswith.htm">fn:endsWith() </a></td><td>判断输入的字符串是否以指定的字符串作为后缀。</td></tr>
<tr><td><a href="/jsp/jstl_function_escapexml.htm">fn:escapeXml() </a></td><td>忽略字符串中的 XML 标签。</td></tr>
<tr><td><a href="/jsp/jstl_function_indexof.htm">fn:indexOf()</a></td><td>返回字符串在指定的字符串第一次出现的位置。</td></tr>
<tr><td><a href="/jsp/jstl_function_join.htm">fn:join() </a></td><td>连接数组中所有的元素到一个字符串中。</td></tr>
<tr><td><a href="/jsp/jstl_function_length.htm">fn:length() </a></td><td>返回集合中的项数或者字符串的字符数。</td></tr>
<tr><td><a href="/jsp/jstl_function_replace.htm">fn:replace()</a></td><td>返回用输入字符串替换到给定的字符串所有出现的位置中所得到的新字符串。</td></tr>
<tr><td><a href="/jsp/jstl_function_split.htm">fn:split()</a></td><td>将一个字符串分割成子字符串数组。</td></tr>
<tr><td><a href="/jsp/jstl_function_startswith.htm">fn:startsWith()</a></td><td>判断输入的字符串是否以指定的字符串作为开头。</td></tr>
<tr><td><a href="/jsp/jstl_function_substring.htm">fn:substring()</a></td><td>返回字符串的子串</td></tr>
<tr><td><a href="/jsp/jstl_function_substringafter.htm">fn:substringAfter()</a></td><td>返回在指定子字符串之前的字符串的子串</td></tr>
<tr><td><a href="/jsp/jstl_function_substringbefore.htm">fn:substringBefore()</a></td><td>返回在指定子字符串之后的字符串的子串</td></tr>
<tr><td><a href="/jsp/jstl_function_tolowercase.htm">fn:toLowerCase()</a></td><td>转换字符串中的所有字符为小写字符 </td></tr>
<tr><td><a href="/jsp/jstl_function_touppercase.htm">fn:toUpperCase()</a></td><td>转换字符串中的所有字符为大写字符</td></tr>
<tr><td><a href="/jsp/jstl_function_trim.htm">fn:trim()</a></td><td>去除字符串两端的空格</td></tr>
</table>



