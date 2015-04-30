# 文件上传 

一个 JSP 可以用一个 HTML 表单标签，它允许用户上传文件到服务器。上传的文件是一个文本文件或二进制文件，图像文件或任何文件。 

## 创建文件上传形式： 

用下面的 HTM 代码创建一个上传表单。以下的要点应该记下来： 
 
- 表单 **method** 的属性应该设置为 **POST** 方法，不能使用 GET 方法。 
- 表单 **enctype** 的属性应该设置为 **multipart/formdata**。

- 表单 **action** 的属性应该设置为一个把文件上传到后台服务器的 JSP 文件。下面的例子是使用程序 **uploadFile.jsp** 来上传文件。

- 为了上传一个单一的文件，你应该使用一个带有属性type="file"的<input .../>标签。为了允许多个文件上传，包含多个输入标签，它们带有不同的name属性的值。浏览器将浏览按钮与每个输入标签进行关联。 

<pre class="prettyprint notranslate tryit"> 
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;File Uploading Form&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;h3&gt;File Upload:&lt;/h3&gt;
Select a file to upload: &lt;br /&gt;
&lt;form action="UploadServlet" method="post"
                        enctype="multipart/form-data"&gt;
&lt;input type="file" name="file" size="50" /&gt;
&lt;br /&gt;
&lt;input type="submit" value="Upload File" /&gt;
&lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

它将显示如下结果，它允许从本地电脑中选择一个文件，当用户点击“Upload File”，
表单将连同选中的文件提交：

<pre class="result notranslate"> 
<b>File Upload:</b> 
<p>Select a file to upload: </p> 
<input type="file" name="file" size="50" /> 
<br /> 
<input type="button" value="Upload File" /> 
<br /> 
</pre>


注意：以上的表单仅仅是虚拟的表单，不能运行，你应该尝试将上述文件放在你的机器中运行。 

## 书写后台 JSP Script: 

首先，让我们定义一个上传文件要存储的位置。你可以在你的程序中进行硬编码或该目录名称也可以使用外部配置来添加，如在 web.xml 的 **context-param** 元素中，如下所示：

``` 
<web-app>
....
<context-param> 
    <description>Location to store uploaded file</description> 
    <param-name>file-upload</param-name> 
    <param-value>
         c:\apache-tomcat-5.5.29\webapps\data\
     </param-value> 
</context-param>
....
</web-app>
```

下面是 UploadFile.jsp 的源代码，它可以一次上传多个文件。处理开始之前，你应该确保下列事项： 

- 下面的例子取决于 FileUpload，所以确保你在 classpath 中有最新的版本 **commons-fileupload.x.x.jar** 文件。你可以从 [http://commons.apache.org/fileupload/](http://commons.apache.org/fileupload/) 中下载它。

- FileUpload 取决于 Commons IO，所以确保你在 classpath 中有最新的版本 **commons-io-x.x.jar** 文件。你可以从 [http://commons.apache.org/io/](http://commons.apache.org/io/) 中下载它。

- 当测试下面的例子时，你应该上传小于 maxFileSize 的文件，否则文件不能上传。

- 确保你提前创建好目录 c:\temp 和 c:\apache-tomcat-5.5.29\webapps\data。

``` 
<%@ page import="java.io.*,java.util.*, javax.servlet.*" %>
<%@ page import="javax.servlet.http.*" %>
<%@ page import="org.apache.commons.fileupload.*" %>
<%@ page import="org.apache.commons.fileupload.disk.*" %>
<%@ page import="org.apache.commons.fileupload.servlet.*" %>
<%@ page import="org.apache.commons.io.output.*" %>
<%
   File file ;
   int maxFileSize = 5000 * 1024;
   int maxMemSize = 5000 * 1024;
   ServletContext context = pageContext.getServletContext();
   String filePath = context.getInitParameter("file-upload");
   // Verify the content type
   String contentType = request.getContentType();
   if ((contentType.indexOf("multipart/form-data") >= 0)) {
      DiskFileItemFactory factory = new DiskFileItemFactory();
      // maximum size that will be stored in memory
      factory.setSizeThreshold(maxMemSize);
      // Location to save data that is larger than maxMemSize.
      factory.setRepository(new File("c:\\temp"));
      // Create a new file upload handler
      ServletFileUpload upload = new ServletFileUpload(factory);
      // maximum file size to be uploaded.
      upload.setSizeMax( maxFileSize );
      try{ 
         // Parse the request to get file items.
         List fileItems = upload.parseRequest(request);
         // Process the uploaded file items
         Iterator i = fileItems.iterator();
         out.println("<html>");
         out.println("<head>");
         out.println("<title>JSP File upload</title>");  
         out.println("</head>");
         out.println("<body>");
         while ( i.hasNext () ) 
         {
            FileItem fi = (FileItem)i.next();
            if ( !fi.isFormField () )	
            {
            // Get the uploaded file parameters
            String fieldName = fi.getFieldName();
            String fileName = fi.getName();
            boolean isInMemory = fi.isInMemory();
            long sizeInBytes = fi.getSize();
            // Write the file
            if( fileName.lastIndexOf("\\") >= 0 ){
            file = new File( filePath + 
            fileName.substring( fileName.lastIndexOf("\\"))) ;
            }else{
            file = new File( filePath + 
            fileName.substring(fileName.lastIndexOf("\\")+1)) ;
            }
            fi.write( file ) ;
            out.println("Uploaded Filename: " + filePath + 
            fileName + "<br>");
            }
         }
         out.println("</body>");
         out.println("</html>");
      }catch(Exception ex) {
         System.out.println(ex);
      }
   }else{
      out.println("<html>");
      out.println("<head>");
      out.println("<title>Servlet upload</title>");  
      out.println("</head>");
      out.println("<body>");
      out.println("<p>No file uploaded</p>"); 
      out.println("</body>");
      out.println("</html>");
   }
%>
```

现在尝试用你在上面创建的 HTML 表单来上传文件。当你运行 http://localhost:8080/UploadFile.htm，它将显示如下结果，它将帮助你从本地电脑上上传任意文件。

<pre class="result notranslate"> 
<b>File Upload:</b> 
<p>Select a file to upload: </p> 
<input type="file" name="file" size="50" /> 
<br /> 
<input type="button" value="Upload File" /> 
</pre>


如果你的 JSP script 运行良好，你的文件应该上传到 c:\apache-tomcat-5.5.29\webapps\data\ directory 中。

