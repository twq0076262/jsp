# JSP - 国际化

在我们继续讨论之前，让我来解释以下三个重要的条目：


- **国际化（i 18 n）:** 这意味着可以使网站根据访问者的语言或者国籍翻译成不同版本的内容。

- **本地化（I 10 n）：** 这意味着将资源添加到一个网站来适应特定的地理或文化，例如将印度语添加到网站。

- **局部区域：** 这是一个特定的文化或地理区域。它通常被称为一个语言符号，该语言符号紧随其后的是一个国家符号，它们之间用下划线分隔。例如，“en_US”代表美国的英语语言环境。

当创建一个全球性的网站时，有很多条目都需要考虑到。本教程在这方面不会提供给你完整的细节，但是在你如何很据互联网社区所在的位置，也就是局部环境，来向它们提供不同语言的网页方面，它会给你一个很好的例子。

一个 JSP 可以根据请求者的区域位置来收集适当的网站版本，并且根据当地语言、文化和需求来提供适当的网站版本。下面是请求对象返回局部区域对象的方法。

```
java.util.Locale request.getLocale() 
```

## 检测局部区域 

以下是重要的局部区域的方法，你可以用来检测请求者的位置、语言和语言环境。以下所有方法显示设置在请求者的浏览器上的国家名称和语言名称。

<table class="table table-bordered"> 
	<tr><th style="width:5%">S.N.</th><th>方法及描述</th></tr> 
	<tr><td>1</td><td><p><b>String getCountry()</b></p> 
	<p>该方法返回国家/地区的代码，用大写的 ISO 3166 2- 字符格式表示语言环境。</p></td></tr> 
	<tr><td>2</td><td><p><b>String getDisplayCountry()</b></p> 
	<p>该方法返回一个局部区域境的国家名称，该名称适合显示给用户。</p></td></tr> 
	<tr><td>3</td><td><p><b>String getLanguage()</b></p> 
	<p>该方法为局部区域用 ISO 639 格式返回小写的语言代码。</p></td></tr> 
	<tr><td>4</td><td><p><b>String getDisplayLanguage()</b></p> 
	<p>该方法返回一个局部区域的语言名称，该名称可以适合显示给用户。</p></td></tr> 
	<tr><td>5</td><td><p><b>String getISO3Country()</b></p> 
	<p>该方法返回一个局部区域国家的三个字母的缩写。</p></td></tr> 
	<tr><td>6</td><td><p><b>String getISO3Language()</b></p> 
	<p>该方法返回一个局部区域语言的三个字母的缩写。</p></td></tr> 
	</table> 

## 例子 

这个例子展示了你如何为 JSP 中的一个请求显示一个语言和与其相关的国家：

```
<%@ page import="java.io.*,java.util.Locale" %>
<%@ page import="javax.servlet.*,javax.servlet.http.* "%>
<%
   //Get the client's Locale
   Locale locale = request.getLocale();
   String language = locale.getLanguage();
   String country = locale.getCountry();
%>
<html>
<head>
<title>Detecting Locale</title>
</head>
<body>
<center>
<h1>Detecting Locale</h1>
</center>
<p align="center">
<% 
   out.println("Language : " + language  + "<br />");
   out.println("Country  : " + country   + "<br />");
%>
</p>
</body>
</html>
```

## 语言设置  

一个 JSP 可以输出一个用西方欧洲语言编写的页面，比如英语、西班牙语、德语、法语、意大利语、荷兰语等等。在这里，适当的设置内容语言标题来显示所有的字符是很重要的。

第二点是使用 HTML 实体显示所有的特殊字符，例如，"&amp;#241;" 代表"&#241;"，"&amp;#161;"代表 “&#161;”，如下：


```
<%@ page import="java.io.*,java.util.Locale" %>
<%@ page import="javax.servlet.*,javax.servlet.http.* "%>
<%
    // Set response content type
    response.setContentType("text/html");
    // Set spanish language code.
    response.setHeader("Content-Language", "es");
    String title = "En Español";

%>
<html>
<head>
<title><%  out.print(title); %></title>
</head>
<body>
<center>
<h1><%  out.print(title); %></h1>
</center>
<div align="center">
<p>En Español</p>
<p>¡Hola Mundo!</p>
</div>
</body>
</html>
```

## 局部区域的特定的日期 

你可以使用 java.text.DateFormat 类和它的静态 getDateTimeinstance() 方法来为局部区域格式化日期和时间特性。下面的例子显示了对于一个给定的局部区域，如何格式化日期特性：

```
<%@ page import="java.io.*,java.util.Locale" %>
<%@ page import="javax.servlet.*,javax.servlet.http.* "%>
<%@ page import="java.text.DateFormat,java.util.Date" %>

<%
    String title = "Locale Specific Dates";
    //Get the client's Locale
    Locale locale = request.getLocale( );
    String date = DateFormat.getDateTimeInstance(
                                  DateFormat.FULL, 
                                  DateFormat.SHORT, 
                                  locale).format(new Date( ));
%>
<html>
<head>
<title><% out.print(title); %></title>
</head>
<body>
<center>
<h1><% out.print(title); %></h1>
</center>
<div align="center">
<p>Local Date: <%  out.print(date); %></p>
</div>
</body>
</html>
```

## 局部区域特定的货币 

在一个局部区域特定的货币，你可以使用 java.txt.NumberFormat 类和它的静态方法 getCurrencyinstance() 来格式化一个数量值，例如一个长型或双精度类型。下面的例子显示了对于一个给定的局部区域，如何格式化货币特性：


```
<%@ page import="java.io.*,java.util.Locale" %>
<%@ page import="javax.servlet.*,javax.servlet.http.* "%>
<%@ page import="java.text.NumberFormat,java.util.Date" %>

<%
    String title = "Locale Specific Currency";
    //Get the client's Locale
    Locale locale = request.getLocale( );
    NumberFormat nft = NumberFormat.getCurrencyInstance(locale);
    String formattedCurr = nft.format(1000000);
%>
<html>
<head>
<title><% out.print(title); %></title>
</head>
<body>
<center>
<h1><% out.print(title); %></h1>
</center>
<div align="center">
<p>Formatted Currency: <%  out.print(formattedCurr); %></p>
</div>
</body>
</html>
```

## 局部区域特定的百分比  

你可以使用 java.txt.NumberFormat 类和它的静态方法 getPercentInstance() 来获取局部区域特定的百分比。下面的例子显示了对于一个给定的局部区域，如何格式化百分比特性：

```
<%@ page import="java.io.*,java.util.Locale" %>
<%@ page import="javax.servlet.*,javax.servlet.http.* "%>
<%@ page import="java.text.NumberFormat,java.util.Date" %>

<%
    String title = "Locale Specific Percentage";
    //Get the client's Locale
    Locale locale = request.getLocale( );
    NumberFormat nft = NumberFormat.getPercentInstance(locale);
    String formattedPerc = nft.format(0.51);
%>
<html>
<head>
<title><% out.print(title); %></title>
</head>
<body>
<center>
<h1><% out.print(title); %></h1>
</center>
<div align="center">
<p>Formatted Percentage: <%  out.print(formattedPerc); %></p>
</div>
</body>
</html>
```



