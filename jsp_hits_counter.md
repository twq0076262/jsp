# 点击计数器 

一个点击计数器告诉你关于网站某个特定页面的访问量。假设人们第一次登陆你的主页，通常你在 index.jsp 页面上设置一个点击计数器。 

你可以使用 Application 隐式对象和相关方法 getAttribute() 和 setAttribute() 实现一个点击计数器。 

这个对象通过其整个生命周期来表示此 JSP 页面。初始化这个对象时创建 JSP 页面，当此 JSP 页面被 jspDestroy() 方法删除时该对象也被删除。 

以下是在应用层设置变量的语法：

```
application.setAttribute(String Key, Object Value);
```

你可以使用上述的方法设置点击计数器的变量或者重置相同的变量。接下来描述的是一个方法，该方法是读取先前方法设置的变量。 

``` 
application.getAttribute(String Key);
```

每次用户访问网页，你可以读取点击计数器的当前值，增加 1 并且再次设置点击计数器作为以后使用。

## 例子：

这个例子展示了如何使用 JSP 来统计一个特定的页面的点击量。如果你想计算你的网站点击量，那么你将不得不在所有 JSP 页面包含相同的代码。 

<pre class="prettyprint notranslate tryit">
&lt;%@ page import="java.io.*,java.util.*" %&gt;

&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Applcation object in JSP&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;%
    Integer hitsCount = 
      (Integer)application.getAttribute("hitCounter");
    if( hitsCount ==null || hitsCount == 0 ){
       /* First visit */
       out.println("Welcome to my website!");
       hitsCount = 1;
    }else{
       /* return visit */
       out.println("Welcome back to my website!");
       hitsCount += 1;
    }
    application.setAttribute("hitCounter", hitsCount);
%&gt;
&lt;center&gt;
&lt;p&gt;Total number of visits: &lt;%= hitsCount%&gt;&lt;/p&gt;
&lt;/center&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在将上面的代码放在 main.jsp 中，并且使用 URL http://localhost:8080/main.jsp 来调用此 JSP。每当你刷新该页面时，这将显示的点击计数器值会增加。你可以尝试使用不同的浏览器访问该网页，你会发现每次点击计数器将增加，显示的结果如下：

<pre class="result notranslate">
<center>
<p>Welcome back to my website!</p>
<p>Total number of visits: 12</p>
</center>
</pre>


## 计数器重置： 

如果你重新启动你的应用程序如 Web 服务器，这将重置你的应用程序变量，点击计数器将重置为零。为了避免这种损失，你可以用下面专业的方法实现点击计数器： 

- 定义一个带有单一计数的数据库表，我们叫做点击量。设置它的值为 0。

- 每次点击，读取该表得到点击量的值。

- 点击量加 1，更新该表中的值。

- 显示点击计数器的新值作为总页面的点击量。

- 如果你想计算所有页面的点击量，对所有的页面实现上面的逻辑。

