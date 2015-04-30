# JSP——发送电子邮件 

用一个 JSP 页面发送邮件虽然足够简单，但是开始你应该有 **JavaMail API**，而且在你的电脑上安装 **Java Activation Framework (JAF)**。 

- 你可以从Java官方网站下载 JavaMail 最新的版本 [JavaMail (Version 1.2)](http://java.sun.com/products/javamail/)。

- 你可以从 Java 官方网站下载 JavaBeans Activation Framework 最新的版本 [JAF (Version 1.0.2)](http://www.oracle.com/technetwork/java/javase/jaf-136260.html)。 

下载和解压这些文件，对于所有的应用程序，在新建的顶层目录中你将可以发现许多 jar 文件。你需要在 CLASSPATH 中添加 **mail.jar** 和 **activation.jar** 文件。 

## 发送一个简单的电子邮件： 

给出一个简单的例子，从你的机器上发送一个简单的邮件。假设你的**本地主机**连接到互联网，能够足以发送一封电子邮件。同时确保所有 jar 文件从 Java Email API 包到 JAF 包在 CLASSPATH 都是可用的。

<pre class="prettyprint notranslate tryit">
&lt;%@ page import="java.io.*,java.util.*,javax.mail.*"%&gt;
&lt;%@ page import="javax.mail.internet.*,javax.activation.*"%&gt;
&lt;%@ page import="javax.servlet.http.*,javax.servlet.*" %&gt;
&lt;%
   String result;
   // Recipient's email ID needs to be mentioned.
   String to = "abcd@gmail.com";

   // Sender's email ID needs to be mentioned
   String from = "mcmohd@gmail.com";

   // Assuming you are sending email from localhost
   String host = "localhost";

   // Get system properties object
   Properties properties = System.getProperties();

   // Setup mail server
   properties.setProperty("mail.smtp.host", host);

   // Get the default Session object.
   Session mailSession = Session.getDefaultInstance(properties);

   try{
      // Create a default MimeMessage object.
      MimeMessage message = new MimeMessage(mailSession);
      // Set From: header field of the header.
      message.setFrom(new InternetAddress(from));
      // Set To: header field of the header.
      message.addRecipient(Message.RecipientType.TO,
                               new InternetAddress(to));
      // Set Subject: header field
      message.setSubject("This is the Subject Line!");
      // Now set the actual message
      message.setText("This is actual message");
      // Send message
      Transport.send(message);
      result = "Sent message successfully....";
   }catch (MessagingException mex) {
      mex.printStackTrace();
      result = "Error: unable to send message....";
   }
%&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Send Email using JSP&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;Send Email using JSP&lt;/h1&gt;
&lt;/center&gt;
&lt;p align="center"&gt;
&lt;% 
   out.println("Result: " + result + "\n");
%&gt;
&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在将上面的代码放在 SendEmail.jsp 文件，并且使用 URL http://localhost:8080/SendEmail.jsp 来调用此 JSP，将电子邮件发送到给定的邮箱 ID 为 abcd@gmail.com 中，显示的响应结果如下所示。

<pre class="result notranslate">
<h1 align="center">Send Email using JSP</h1>
<p align="center">Result: Sent message successfully....</p>
</pre>


如果你想给多个收件人发送邮件，下面的方法可用于发送邮件给指定的多个邮箱 IDs：

``` 
void addRecipients(Message.RecipientType type, 
                   Address[] addresses)
throws MessagingException
```

下面是对参数的描述： 

- **type：** 可设置为 TO，CC 或者 BCC。其中，CC 表示 Carbon Copy，BCC 表示 Black Carbon Copy。例如，*Message.RecipientType.TO*。

- **addresses:** 它是邮箱 ID 的数组。你能使用 InternetAddress() 方法，同时指定邮箱 IDs。

## 发送 HTML 邮件： 

给出一个简单的例子，从你的机器上发送一个网页邮件。假设你的**本地主机**连接到互联网，能够足以发送一封电子邮件。同时确保所有 jar 文件从 Java Email API 包到 JAF 包在 CLASSPATH 都是可用的。 

这个例子与之前给出的例子非常相似，除了在这个例子中我们使用 setContent() 方法设置第二个参数为“text/html”，用来指定网页内容包含在这个信息中。 

使用这个例子，你可以发送与你喜欢的网页内容一样大的邮件。

<pre class="prettyprint notranslate">
&lt;%@ page import="java.io.*,java.util.*,javax.mail.*"%&gt;
&lt;%@ page import="javax.mail.internet.*,javax.activation.*"%&gt;
&lt;%@ page import="javax.servlet.http.*,javax.servlet.*" %&gt;
&lt;%
   String result;
   // Recipient's email ID needs to be mentioned.
   String to = "abcd@gmail.com";

   // Sender's email ID needs to be mentioned
   String from = "mcmohd@gmail.com";

   // Assuming you are sending email from localhost
   String host = "localhost";

   // Get system properties object
   Properties properties = System.getProperties();

   // Setup mail server
   properties.setProperty("mail.smtp.host", host);

   // Get the default Session object.
   Session mailSession = Session.getDefaultInstance(properties);

   try{
      // Create a default MimeMessage object.
      MimeMessage message = new MimeMessage(mailSession);
      // Set From: header field of the header.
      message.setFrom(new InternetAddress(from));
      // Set To: header field of the header.
      message.addRecipient(Message.RecipientType.TO,
                               new InternetAddress(to));
      // Set Subject: header field
      message.setSubject("This is the Subject Line!");
     
      // Send the actual HTML message, as big as you like
      message.setContent("&lt;h1&gt;This is actual message&lt;/h1&gt;",
                            "text/html" );
      // Send message
      Transport.send(message);
      result = "Sent message successfully....";
   }catch (MessagingException mex) {
      mex.printStackTrace();
      result = "Error: unable to send message....";
   }
%&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Send HTML Email using JSP&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;Send Email using JSP&lt;/h1&gt;
&lt;/center&gt;
&lt;p align="center"&gt;
&lt;% 
   out.println("Result: " + result + "\n");
%&gt;
&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在可以使用上述 JSP 发送网页信息给指定的邮箱 ID。 

## 在电子邮件中发送附件： 

给定一个例子，从你的机器上发送一个带附件的邮箱：

<pre class="prettyprint notranslate">
&lt;%@ page import="java.io.*,java.util.*,javax.mail.*"%&gt;
&lt;%@ page import="javax.mail.internet.*,javax.activation.*"%&gt;
&lt;%@ page import="javax.servlet.http.*,javax.servlet.*" %&gt;
&lt;%
   String result;
   // Recipient's email ID needs to be mentioned.
   String to = "abcd@gmail.com";

   // Sender's email ID needs to be mentioned
   String from = "mcmohd@gmail.com";

   // Assuming you are sending email from localhost
   String host = "localhost";

   // Get system properties object
   Properties properties = System.getProperties();

   // Setup mail server
   properties.setProperty("mail.smtp.host", host);

   // Get the default Session object.
   Session mailSession = Session.getDefaultInstance(properties);

   try{
      // Create a default MimeMessage object.
      MimeMessage message = new MimeMessage(mailSession);

      // Set From: header field of the header.
      message.setFrom(new InternetAddress(from));

      // Set To: header field of the header.
      message.addRecipient(Message.RecipientType.TO,
                               new InternetAddress(to));

      // Set Subject: header field
      message.setSubject("This is the Subject Line!");

      // Create the message part 
      BodyPart messageBodyPart = new MimeBodyPart();

      // Fill the message
      messageBodyPart.setText("This is message body");
      
      // Create a multipar message
      Multipart multipart = new MimeMultipart();

      // Set text message part
      multipart.addBodyPart(messageBodyPart);

      // Part two is attachment
      messageBodyPart = new MimeBodyPart();
      String filename = "file.txt";
      DataSource source = new FileDataSource(filename);
      messageBodyPart.setDataHandler(new DataHandler(source));
      messageBodyPart.setFileName(filename);
      multipart.addBodyPart(messageBodyPart);

      // Send the complete message parts
      message.setContent(multipart );

      // Send message
      Transport.send(message);
      String title = "Send Email";
      result = "Sent message successfully....";
   }catch (MessagingException mex) {
      mex.printStackTrace();
      result = "Error: unable to send message....";
   }
%&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Send Attachement Email using JSP&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;center&gt;
&lt;h1&gt;Send Attachement Email using JSP&lt;/h1&gt;
&lt;/center&gt;
&lt;p align="center"&gt;
&lt;% 
   out.println("Result: " + result + "\n");
%&gt;
&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>


现在可以运行上述 JSP 发送一个文件作为信息的附件给指定邮箱 ID。 

## 用户身份验证部分： 

为了身份验证的目的，如果需要提供用户 ID 和密码给邮箱服务器，你可以设置这些属性如下：

``` 
props.setProperty("mail.user", "myuser");
 props.setProperty("mail.password", "mypwd");
```

邮件发送机制的设置和上述的解释一致。 

## 用表单发送邮件： 

你可以使用网页表单接受邮件参数，然后你可以使用 request 对象获得如下的所有信息：

``` 
String to = request.getParameter("to");
String from = request.getParameter("from");
String subject = request.getParameter("subject");
String messageText = request.getParameter("body");
```

一旦你有所有信息，你可以使用以上提到的代码发送邮件。
