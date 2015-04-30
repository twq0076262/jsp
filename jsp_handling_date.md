# 处理日期 

使用 JSP 的一个最重要的优点是，你可以使用核心 Java 中所有有效的方法。本教程将教你使用 Java 提供的 **Date** 类，它在 **java.util** 包是有效的，这个类封装了当前的日期和时间。 

这个 Date 类支持两种构造函数。第一种构造函数是初始化当前日期和时间的对象。

``` 
Date( )
```

下面的构造函数是设置一个参数，该参数是从 1970 年 1 月 1 日凌晨 0 点开始至今的毫秒数。 

``` 
Date(long millisec)
```

一旦你有一个有效的 Date 对象，你可以调用以下任何支持的方法实现日期： 

<table class="table table-bordered">
<tr>
<th style="width:5%">SN</th><th style="width:95%">方法描述</th></tr>
<tr><td>1</td><td><p><b>boolean after(Date date)</b></p>
<p>如果调用的 Date 对象包含的日期晚于指定的日期，则返回 true，否则返回 false。</p></td></tr>
<tr><td>2</td><td><p><b>boolean before(Date date)</b></p>
<p>如果调用的 Date 对象包含的日期早于指定的日期，则返回 true，否则返回 false。</p></td></tr>
<tr><td>3</td><td><p><b>Object clone( )</b></p>
<p>重复调用的 Date 对象。</p></td></tr>
<tr><td>4</td><td><p><b>int compareTo(Date date)</b></p>
<p>比较调用的 Date 对象与 date 的值。如果值是相等的，则返回 0。如果调用的 Date 对象比 date 更早，则返回一个负数。如果调用 Date 对象是晚于 date 的，则返回一个正数。</p></td></tr>
<tr><td>5</td><td><p><b>int compareTo(Object obj)</b></p>
<p>如果 obj 是 Date 类，则操作与 compareTo(Date) 是同一个，否则抛出 ClassCastException 异常。</p></td></tr>
<tr><td>6</td><td><p><b>boolean equals(Object date)</b></p>
<p>如果调用的 Date 对象与指定的日期有相同的时间和日期，则返回 true，否则返回 false。</p></td></tr>
<tr><td>7</td><td><p><b>long getTime( )</b></p>
<p>返回从 1970 年 1 月 1 日凌晨 0 点开始至今的毫秒数。</p></td></tr>
<tr><td>8</td><td><p><b>int hashCode( )</b></p>
<p>返回调用对象的哈希编码</p></td></tr>
<tr><td>9</td><td><p><b>void setTime(long time)</b></p>
<p>由指定的时间设置时间和日期，它表示从 1970 年 1 月 1 日凌晨 0 点开始到指定时间的毫秒数。</p></td></tr>
<tr><td>10</td><td><p><b>String toString( )</b></p>
<p>转换调用的 Date 对象到 string 类型，并且返回该结果。</p></td></tr>
</table>


## 得到当前日期 & 时间： 

在 JSP 程序中，很容易得到当前日期和时间。你可以使用一个简单的 Date 对象调用 toString() 方法来输出当前的日期和时间，如下所示：

<pre class="prettyprint notranslate tryit">
&lt;%@ page import="java.io.*,java.util.*, javax.servlet.*" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Display Current Date &amp; Time&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;Display Current Date &amp; Time&lt;/h1&gt;
&lt;/center&gt;
&lt;%
   Date date = new Date();
   out.print( "&lt;h2 align=\"center\"&gt;" +date.toString()+"&lt;/h2&gt;");
%&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在我们将保持 CurrentDate.jsp 中代码，然后使用 URL http://localhost:8080/CurrentDate.jsp 来调用此 JSP。将产生如下结果：

<pre class="result notranslate">
<h1 align="center">Display Current Date &amp; Time</h1>
<h2 align="center">Mon Jun 21 21:46:49 GMT+04:00 2010</h2>
</pre>


尝试刷新 URL http://localhost:8080/CurrentDate.jsp，你将会发现每一次刷新都会有几秒钟的区别。 

## 日期比较： 

正如上面提到的，你可以使用所有有效的 Java 方法在你的 JavaScript 中。如果你需要比较两个日期，下面是方法： 

- 你可以用 getTime() 方法分别获得这两个对象从 1970 年 1 月 1 日凌晨 0 点开始至今的毫秒数，然后比较这两个值。

- 你可以使用方法 before()，after() 和 equals()。因为每月的 12 日在 18 日之前，例如，new Date(99,2,12).(new Date(99,2,18))，返回 true。

- 你可以使用 compareTo() 方法，它由 Comparable 接口定义并且有 Date 实现。

## 用 SimpleDateFormat 实现日期格式化： 

SimpleDateFormat 是用对语言环境敏感的方式来格式化和解析日期的具体类。SimpleDateFormat 允许你对日期时间格式来选择任何用户定义的模式开始。 

让我们修改上面的例子，如下所示：

<pre class="prettyprint notranslate tryit">
&lt;%@ page import="java.io.*,java.util.*" %&gt;
&lt;%@ page import="javax.servlet.*,java.text.*" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Display Current Date &amp; Time&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;Display Current Date &amp; Time&lt;/h1&gt;
&lt;/center&gt;
&lt;%
   Date dNow = new Date( );
   SimpleDateFormat ft = 
   new SimpleDateFormat ("E yyyy.MM.dd 'at' hh:mm:ss a zzz");
   out.print( "&lt;h2 align=\"center\"&gt;" + ft.format(dNow) + "&lt;/h2&gt;");
%&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


再次编译上述 Servlet，然后使用 URL http://localhost:8080/CurrentDate 来调用此 Servlet。将产生如下结果： 

<pre class="result notranslate">
<h1 align="center">Display Current Date &amp; Time</h1>
<h2 align="center">Mon 2010.06.21 at 10:06:44 PM GMT+04:00</h2>
</pre>


## Simple DateFormat 格式化代码： 

指定时间格式使用一个时间模式字符串。在这个模式中,所有 ASCII 字母被保留为模式字母，它们被定义为如下： 

<table class="table table-bordered">
<tr><th style="width:10%">字符</th><th style="width:45%">描述</th><th>例子</th>
</tr>
<tr><td>G</td><td>时代指示符</td><td>AD</td></tr>
<tr><td>y</td><td>四位数的某年</td><td>2001</td></tr>
<tr><td>M</td><td>一年中的某月</td><td>July or 07</td></tr>
<tr><td>d</td><td>一月中的某日</td><td>10</td></tr>
<tr><td>h</td><td>A.M./P.M. (1~12)的某小时</td><td>12</td></tr>
<tr><td>H</td><td>一天 (0~23)中的某小时</td><td>22</td></tr>
<tr><td>m</td><td>一小时中的某分钟</td><td>30</td></tr>
<tr><td>s</td><td>一分钟中的某秒</td><td>55</td></tr>
<tr><td>S</td><td>毫秒</td><td>234</td></tr>
<tr><td>E</td><td>一周中的某天</td><td>Tuesday</td></tr>
<tr><td>D</td><td>一年中的某天</td><td>360</td></tr>
<tr><td>F</td><td>一月中的一周的某天</td><td>2 (second Wed. in July)</td></tr>
<tr><td>w</td><td>一年中的某周</td><td>40</td></tr>
<tr><td>W</td><td>一月中的某周</td><td>1</td></tr>
<tr><td>a</td><td>A.M./P.M.标记</td><td>PM</td></tr>
<tr><td>k</td><td>一天(1~24)中的某小时</td><td>24</td></tr>
<tr><td>K</td><td>A.M./P.M. (0~11)的某小时</td><td>10</td></tr>
<tr><td>z</td><td>时区</td><td>Eastern Standard Time</td></tr>
<tr><td>'</td><td>消逝的文本</td><td>Delimiter</td></tr>
<tr><td>"</td><td>单引号</td><td>`</td></tr>
</table>

对于一个用不变且有效的方法来操作日期的完整清单，你可以参考标准的 Java 文件。

