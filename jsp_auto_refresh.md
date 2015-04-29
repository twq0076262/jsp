# JSP——自动刷新

细想一个显示在线比赛分数、股市状态或当前交易额的网页。对于所有这种类型的网页，你需要通过浏览器中的更新或者重新载入按钮定期的刷新网页。

通过提供一个在给定的间距后自动刷新网页的机制，可以使 JSP 更加容易运行。 

刷新网页最简单的方法就是使用 request 对象的 **setIntHeader()** 方法。下面是这个方法的符号描述：

``` 
public void setIntHeader(String header, int headerValue)
```

此方法将标题“刷新”以及以秒为单位的时间间隔的整数值返回给浏览器。 

## 自动页面刷新例子： 

下面的例子使用 **setIntHeader()** 方法设置 **Refresh** 标头来模拟数字计时器：

<pre class="prettyprint notranslate tryit">
&lt;%@ page import="java.io.*,java.util.*" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Auto Refresh Header Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h2&gt;Auto Refresh Header Example&lt;/h2&gt;
&lt;%
   // Set refresh, autoload time as 5 seconds
   response.setIntHeader("Refresh", 5);
   // Get current time
   Calendar calendar = new GregorianCalendar();
   String am_pm;
   int hour = calendar.get(Calendar.HOUR);
   int minute = calendar.get(Calendar.MINUTE);
   int second = calendar.get(Calendar.SECOND);
   if(calendar.get(Calendar.AM_PM) == 0)
      am_pm = "AM";
   else
      am_pm = "PM";
   String CT = hour+":"+ minute +":"+ second +" "+ am_pm;
   out.println("Crrent Time: " + CT + "\n");
%&gt;
&lt;/center&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在将上面的代码放在 main.jsp 中，并且访问它。它将在之后每隔 5 s 显示当前系统时间。只运行此 JSP 页面，等待一会可以看到如下结果：

<pre class="result notranslate">
<center>
<h2 align="center">Auto Refresh Header Example</h2>
Current Time is: 9:44:50 PM
</center>
</pre>


为了变得与其他方法更加合适，你可以用同样的形式尝试更多上面列出的方法。

