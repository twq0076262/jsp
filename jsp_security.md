# JSP——安全性

JavaServer Pages 和 servlets 有几种可用的机制可以使 web 开发人员用来保护应用程序。资源可以通过在应用程序部署描述中对它们进行识别并且为它们分配一个角色来声明式地保护它们。 

有几种级别的身份验证是可用的，从使用基本标示符的基本验证到复杂的使用证书的密码验证。 

## 基本角色的验证：

Servlet 规范中的认证机制使用的是一项被称为基于角色的安全技术。该想法是你通过角色来创建角色和限制资源，而不是限制用户级别的资源。

你可以定义在文件 tomcat-users.xml 中定义不同的角色，该文件位于 Tomcat 的主页目录中的 conf. 中。此文件的一个示例如下所示：

``` 
<?xml version='1.0' encoding='utf-8'?>
<tomcat-users>
<role rolename="tomcat"/>
<role rolename="role1"/>
<role rolename="manager"/>
<role rolename="admin"/>
<user username="tomcat" password="tomcat" roles="tomcat"/>
<user username="role1" password="tomcat" roles="role1"/>
<user username="both" password="tomcat" roles="tomcat,role1"/>
<user username="admin" password="secret" roles="admin,manager"/>
</tomcat-users>
```

这个文件在用户名称、密码和角色之间定义了一个简单的映射。请注意，一个给定的用户可能有多个角色，例如，在“tomcat”角色中的用户名=“both”，角色是“role1”。

一旦你识别和定义了不同的角色，一个基于角色的安全限制可以通过使用 <security-constraint> 元素被放置在不同的 web 应用程序中，该元素在 WEB-INF 目录中的 web.xml 文件中是可用的。

下面是 web.xml 中一个简单的示例：

``` 
<web-app>
...
    <security-constraint>
        <web-resource-collection>
            <web-resource-name>
               SecuredBookSite
            </web-resource-name>
            <url-pattern>/secured/*</url-pattern>
            <http-method>GET</http-method>
            <http-method>POST</http-method>
        </web-resource-collection>
        <auth-constraint>
            <description>
            Let only managers use this app
            </description>
            <role-name>manager</role-name>
        </auth-constraint>
    </security-constraint>
    <security-role>
  	   <role-name>manager</role-name>
    </security-role>
    <login-config>
      <auth-method>BASIC</auth-method>
    </login-config>
...
</web-app>
```

以上条目将意味着：

- 任何 通过 /secured/* 对一个 URL匹配 的HTTP GET 或者 POST 请求都将被安全限制所接受。

- 一个有着管理员角色的人是可以访问被保护的资源的。

- 最后，login-config 元素是用来描述身份验证的 BASIC 形式。

现在，如果你试图浏览任何包含  /security  目录的 URL，它将显示一个询问用户名和密码的对话框。如果你提供一个用户“admin”和密码“secrer”，那么只有你可以通过  /secured/*  访问上面的 URL，因为我们已经定义了用户为管理员角色，而该角色是有权访问该资源的。

## 基于表单的身份验证： 

当时使用表单身份验证方法时，你必须提供一个登录表单来提示用户输入用户名和密码。下面是一个简单登录页面 login.jsp 的代码，用来创建一个相同目的的表单：

<pre class="prettyprint notranslate">
&lt;html&gt;
&lt;body bgcolor="#ffffff"&gt;
   &lt;form method="POST" action="j_security_check"&gt;
      &lt;table border="0"&gt;
      &lt;tr&gt;
      &lt;td&gt;Login&lt;/td&gt;
      &lt;td&gt;&lt;input type="text" name="j_username"&gt;&lt;/td&gt;
      &lt;/tr&gt;
      &lt;tr&gt;
      &lt;td&gt;Password&lt;/td&gt;
      &lt;td&gt;&lt;input type="password" name="j_password"&gt;&lt;/td&gt;
      &lt;/tr&gt;
      &lt;/table&gt;
      &lt;input type="submit" value="Login!"&gt;
      &lt;/center&gt;
   &lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;
 </pre>


在这里，你必须确保登录表单中必须包含以 j_username 和 j_password 命名的表单元素。在 <form> 标签中的动作必须是 j_security_check。POST必须以表单的方法来使用。同时你必须修改 <login-config> 标签来指定 auth-method 作为表单：

``` 
<web-app>
...
    <security-constraint>
        <web-resource-collection>
            <web-resource-name>
               SecuredBookSite
            </web-resource-name>
            <url-pattern>/secured/*</url-pattern>
            <http-method>GET</http-method>
            <http-method>POST</http-method>
        </web-resource-collection>
        <auth-constraint>
            <description>
            Let only managers use this app
            </description>
            <role-name>manager</role-name>
        </auth-constraint>
    </security-constraint>
    <security-role>
  	   <role-name>manager</role-name>
    </security-role>
    <login-config>
      <auth-method>FORM</auth-method>
      <form-login-config>
        <form-login-page>/login.jsp</form-login-page>
        <form-error-page>/error.jsp</form-error-page>
      </form-login-config>
    </login-config>
...
</web-app>
```


现在，当你试图用 URL /secured/* 访问任何资源时，它将显示以上的表单，要求用户 id 和密码。当容器看到“j_security_check”动作时，它会使用一些内部机制来对调用方进行身份验证。

如果登录成功，调用者会被授权访问安全资源，那么从那时起容器会用一个 session-id 来识别调用者的登录会话。容器会用一个包含 session-id 的 cookie 来保持这个登录会话。服务器将 cookie 发送回客户端，并且只要调用者使用后续的请求显示这个 cookie 时，那么容器就会知道这个调用者是谁。

如果登录失败，那么服务器将发回由 form-error-page 设置识别的页面。

这里，j_security_check 是登录表单中使用基于表单登录的应用程序必须指定的一个动作。在相同的表单中，你该应该有一个名为 j_username 的文本输入控件和一个名为 j_password 的密码输入控件。当你看到这，这意味着表单中包含的信息将会被提交到服务器，服务器将会检查用户名和密码。这一步如何实现是由服务器指定的。

检查[ Standard Realm Implementations](http://tomcat.apache.org/tomcat-5.5-doc/realm-howto.html) 来来了解 j_security_check 是如何为 Tomcat 容器工作的。

## Servlet/JSP 中的程序性安全：

HttpServletRequest 对象提供了以下方法，它可以在运行时用于挖掘安全信息：

<table class="table table-bordered"> 
	<tr><th style="width:5">序号</th><th>方法及描述 </th></tr> 
	<tr><td>1</td><td><p><b>String getAuthType()</b></p> 
	<p> getAuthType() 方法返回一个字符串对象，代表用于保护 Servlet 的身份验证方案的名称。</p></td></tr> 
	<tr><td>2</td><td><p><b>boolean isUserInRole(java.lang.String role)</b></p> 
	<p> isUserInRole() 返回一个布尔型的值: 如果用户在给定的角色中值为真，否则值为假。</p></td></tr> 
	<tr><td>3</td><td><p><b>String getProtocol()</b></p> 
	<p> getProtocol() 方法返回一个字符串对象，代表用户发送请求的协议。它的值可以用来检查确定一个保护协议是否被使用。</p></td></tr> 
	<tr><td>4</td><td><p><b>boolean isSecure()</b></p> 
	<p> isSecure() 方法返回一个布尔型的值，代表请求是否是使用的 HTTPS协议。真值代表是并且连接是安全的。假值代表不是。/p></td></tr> 
	<tr><td>5</td><td><p><b>Principle getUserPrinciple()</b></p> 
	<p> getUserPrinciple() 方法返回一个 java.security.Principle 对象，该对象包含当前已验证用户的用户名。</p></td></tr> 
	</table> 

例如，一个 JavaServer Page 连接的是管理员页面，你可能会使用以下代码：

```
<% if (request.isUserInRole("manager")) { %><a href="managers/mgrreport.jsp">Manager Report</a><a href="managers/personnel.jsp">Personnel Records</a><% } %>
```

在一个 JSP 或者 servlet 里，通过检查用户的角色，你可以自定义 web 网页来显示只有用户自己可以访问的条目。如果你需要用户名作为身份验证表单的输入，那么你可以在请求对象中调用 getRemoteUser 方法。
