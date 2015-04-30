# 自定义标签 

自定义标签是一种用户定义的 JSP 语言元素。当一个包含自定义标签的 JSP 页面翻译成一个 servlet 时，该标签转换为在一个对象上的操作称为标签处理程序。然后当执行 JSP 页面的 servlet 时，Web 容器调用这些操作。 

扩展的 JSP 标签允许你创建新标签，你可以直接插入到一个 JavaServer Page（JSP）中，就像在先前章节中学习的内置标签。为了编写这些自定义标签，JSP 2.0 规范引入了简单的标签处理程序。 

要编写一个自定义标签，你可以简单地扩展 SimpleTagSupport 类，并且重写 **doTag( )** 方法，其中你可以添加你的代码来生成标签的内容。 

## 创建“Hello”标签： 

假如你想定义一个自定义标签名为 <ex:Hello>，你想要在以下没有标签体的方式中使用，如下所示：

``` 
<ex:Hello />
```

要创建一个自定义 JSP 标签，你必须首先创建一个 Java 类作为标记处理程序。因此，创建 HelloTag 类如下：

``` 
package com.tutorialspoint;
import javax.servlet.jsp.tagext.*;
import javax.servlet.jsp.*;
import java.io.*;
public class HelloTag extends SimpleTagSupport {
  public void doTag() throws JspException, IOException {
    JspWriter out = getJspContext().getOut();
    out.println("Hello Custom Tag!");
  }
}
```

上面的代码是简单的编码，其中 doTag() 方法使用 getJspContext() 产生的当前 JspWriter 对象，并使用它发送“Hello Custom Tag!”给当前的 JspWriter 对象。

编译上面的类，并将其复制到 CLASSPATH 环境变量的有效目录中。最后创建以下标签库文件：<Tomcat-Installation-Directory>webapps\ROOT\WEB-INF\custom.tld。

``` 
<taglib>
  <tlib-version>1.0</tlib-version>
  <jsp-version>2.0</jsp-version>
  <short-name>Example TLD</short-name>
  <tag>
    <name>Hello</name>
    <tag-class>com.tutorialspoint.HelloTag</tag-class>
    <body-content>empty</body-content>
  </tag>
</taglib>
```

在我们的 JSP 程序中，使用上面定义的自定义标签 Hello，如下所示：

<pre class="prettyprint notranslate">
&lt;%@ taglib prefix="ex" uri="WEB-INF/custom.tld"%&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;A sample custom tag&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;ex:Hello/&gt;
  &lt;/body&gt;
&lt;/html&gt;
</pre>

尝试调用上述JSP，显示结果如下所示：


<pre class="result notranslate">
Hello Custom Tag!
</pre>


## 访问标签体： 

你可以标签体中引用在标准标签体中你所见的消息。假如你想定义一个自定义标签名为 <ex:Hello>，你想要在以下含有标签体的方式中使用，如下所示：

``` 
<ex:Hello>
   This is message body
</ex:Hello>
```

在上面标签的代码中进行如下修改来处理标签的主体：

``` 
package com.tutorialspoint;
import javax.servlet.jsp.tagext.*;
import javax.servlet.jsp.*;
import java.io.*;
public class HelloTag extends SimpleTagSupport {
   StringWriter sw = new StringWriter();
   public void doTag()
      throws JspException, IOException
    {
       getJspBody().invoke(sw);
       getJspContext().getOut().println(sw.toString());
    }
}
```

在这种情况下，在调用中产生的输出是在写入与标签相关的 JspWriter 对象之前第一个捕获到的 StringWriter。因此我们需要改变 TLD 文件，如下所示：

``` 
<taglib>
  <tlib-version>1.0</tlib-version>
  <jsp-version>2.0</jsp-version>
  <short-name>Example TLD with Body</short-name>
  <tag>
    <name>Hello</name>
    <tag-class>com.tutorialspoint.HelloTag</tag-class>
    <body-content>scriptless</body-content>
  </tag>
</taglib>
```

现在让我们调用上述带有标签体的标签，如下所示：

<pre class="prettyprint notranslate">
&lt;%@ taglib prefix="ex" uri="WEB-INF/custom.tld"%&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;A sample custom tag&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;ex:Hello&gt;
        This is message body
    &lt;/ex:Hello&gt;
  &lt;/body&gt;
&lt;/html&gt;
</pre>

显示结果如下所示：

<pre class="result notranslate">
This is message body
</pre>


## 自定义标签属性： 

你可以使用自定义标签的各种属性。要得到一个属性值，一个自定义标签类需要实现 setter 方法，和 JavaBean 相同的 setter 方法如下所示：

``` 
package com.tutorialspoint;
import javax.servlet.jsp.tagext.*;
import javax.servlet.jsp.*;
import java.io.*;
public class HelloTag extends SimpleTagSupport {
   private String message;
   public void setMessage(String msg) {
      this.message = msg;
   }
   StringWriter sw = new StringWriter();
   public void doTag()
      throws JspException, IOException
    {
       if (message != null) {
          /* Use message from attribute */
          JspWriter out = getJspContext().getOut();
          out.println( message );
       }
       else {
          /* use message from the body */
          getJspBody().invoke(sw);
          getJspContext().getOut().println(sw.toString());
       }
   }
}
```

属性的名称是“message”，因此 setter 方法是 setMessage( )。现在让我们用 <attribute> 元素添加该属性到 TLD 文件中，如下所示：

``` 
<taglib>
  <tlib-version>1.0</tlib-version>
  <jsp-version>2.0</jsp-version>
  <short-name>Example TLD with Body</short-name>
  <tag>
    <name>Hello</name>
    <tag-class>com.tutorialspoint.HelloTag</tag-class>
    <body-content>scriptless</body-content>
    <attribute>
       <name>message</name>
    </attribute>
  </tag>
</taglib>
```

现在尝试下面的带有消息属性的 JSP 页面，如下所示：

<pre class="prettyprint notranslate">
&lt;%@ taglib prefix="ex" uri="WEB-INF/custom.tld"%&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;A sample custom tag&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;ex:Hello message="This is custom tag" /&gt;
  &lt;/body&gt;
&lt;/html&gt;
</pre>


显示结果如下所示：

<pre class="result notranslate">
This is custom tag
</pre>


希望上面的例子对你有帮助。值得注意的是，一个属性可以包含下列属性：

<table class="table table-bordered">
<tr><th style="width:30%">属性 </th><th>目的</th></tr>
<tr><td>name</td><td>名称元素定义了一个属性的名称。对于一个特定的标签，每个属性名称必须是唯一。</td></tr>
<tr><td>required</td><td>这指定如果这个属性是必需的或可选的，则指定它。对于可选的，默认为 false。</td></tr>
<tr><td>rtexprvalue</td><td>如果对于一个标签属性，运行时间表达式的值是有效的，则声明它。</td></tr>
<tr><td>type</td><td>定义了该属性的Java类类型。默认情况下它是假设为<b>字符串</b></td></tr>
<tr><td>description</td><td>可以提供信息的描述。</td></tr>
<tr><td>fragment</td><td>如果这个属性值应该被视做一个 <b>JspFragment</b>，则声明它。</td></tr>
</table>


下面是指定一个属性的相关属性的例子：

``` 
.....
    <attribute>
      <name>attribute_name</name>
      <required>false</required>
      <type>java.util.Date</type>
      <fragment>false</fragment>
    </attribute>
.....
```

如果你使用的是两个属性，那么你可以修改你的 TLD 如下所示：

``` 
.....
    <attribute>
      <name>attribute_name1</name>
      <required>false</required>
      <type>java.util.Boolean</type>
      <fragment>false</fragment>
    </attribute>
    <attribute>
      <name>attribute_name2</name>
      <required>true</required>
      <type>java.util.Date</type>
    </attribute>
.....
```