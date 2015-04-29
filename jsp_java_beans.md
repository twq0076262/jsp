# JavaBeans 

JavaBean 是在编写 Java 时专门创建的 Java 类，根据 JavaBean API 规范进行编码 
。
以下是区分 JavaBean 和其他 Java 类的特有的特征： 

- 它提供了一个默认的无参数构造函数。

- 它应该是可序列化的，实现 **serializable** 接口。

- 它可能有大量可以读或写的属性。

- 它可能有大量“getter”和“setter”方法的属性。

## JavaBean 属性： 

JavaBean 属性是一个命名属性，这个属性是用户可以访问的对象。属性可以是任何 Java 数据类型，包括自定义的类。 

JavaBean 属性可以读、写、只读或只写。JavaBean 属性是在 JavaBean 实现类中通过两种方法访问的： 

<table class="table table-bordered">
<tr><th style="width:30%">方法 </th><th>描述</th></tr>
<tr><td>get<b>PropertyName</b>()</td><td>例如，如果属性名称是 firstName，你的方法名称应该是 getFirstName()，它可以读该属性。该方法叫做访问器。</td></tr>
<tr><td>set<b>PropertyName</b>()</td><td>例如，如果属性名称是 firstName，你的方法名称应该是 setFirstName()，它可以写该属性。该方法叫做赋值方法。</td></tr>
</table>


一个只读属性只会有一个 get**PropertyName()** 方法，而一个只写属性将只有一个 set**PropertyName()** 方法。 

## JavaBeans 例子： 

考虑一个带有一些属性的 student 类：

``` 
package com.tutorialspoint;
public class StudentsBean implements java.io.Serializable
{
   private String firstName = null;
   private String lastName = null;
   private int age = 0;
   public StudentsBean() {
   }
   public String getFirstName(){
      return firstName;
   }
   public String getLastName(){
      return lastName;
   }
   public int getAge(){
      return age;
   }
   public void setFirstName(String firstName){
      this.firstName = firstName;
   }
   public void setLastName(String lastName){
      this.lastName = lastName;
   }
   public void setAge(Integer age){
      this.age = age;
   }
}
```

## 访问 JavaBeans： 

在一个 JSP 页面使用时，**useBean** 操作声明一个对象。一旦声明，bean 成为脚本变量，在使用它的 JSP 页面中，它可以通过脚本元素和其他自定义标签访问。useBean 标签的完整的语法如下：

``` 
<jsp:useBean id="bean's name" scope="bean's scope" typeSpec/>
```

根据你的需求，这里 scope 属性值可能是页面、请求、会话或应用程序。**id** 属性的值可以是任何值，在同一个 JSP 页面中，只要它是一个唯一的名字与其他 useBean 声明。 

下面的例子显示了其简单的用法：

<pre class="prettyprint notranslate tryit">
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;useBean Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;jsp:useBean id="date" class="java.util.Date" /&gt; 
&lt;p&gt;The date/time is &lt;%= date %&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>


产生的结果如下所示：

<pre class="result notranslate">
The date/time is Thu Sep 30 11:18:11 GST 2010 
</pre>


## 访问 javabean 属性： 

随着 < jsp:useBean…>，你可以使用 < jsp:getProperty / > 操作来访问方法和 < jsp:setProperty / > 操作来访问设置方法。这是完整的语法：

``` 
<jsp:useBean id="id" class="bean's class" scope="bean's scope">
   <jsp:setProperty name="bean's id" property="property name"  
                    value="value"/>
   <jsp:getProperty name="bean's id" property="property name"/>
   ...........
</jsp:useBean>
```

该名称属性通过 useBean 操作把先前介绍 JavaBean 的 id 引用到 JSP 页面中。该属性的属性是应该被调用 get 或 set 方法的名称。 

下面是一个使用上面的语法访问数据的简单的例子：

<pre class="prettyprint notranslate tryit">
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;get and set properties Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;jsp:useBean id="students" 
                    class="com.tutorialspoint.StudentsBean"&gt; 
   &lt;jsp:setProperty name="students" property="firstName"
                    value="Zara"/&gt;
   &lt;jsp:setProperty name="students" property="lastName" 
                    value="Ali"/&gt;
   &lt;jsp:setProperty name="students" property="age" 
                    value="10"/&gt;
&lt;/jsp:useBean&gt;

&lt;p&gt;Student First Name: 
   &lt;jsp:getProperty name="students" property="firstName"/&gt;
&lt;/p&gt;
&lt;p&gt;Student Last Name: 
   &lt;jsp:getProperty name="students" property="lastName"/&gt;
&lt;/p&gt;
&lt;p&gt;Student Age: 
   &lt;jsp:getProperty name="students" property="age"/&gt;
&lt;/p&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>


让我们在 CLASSPATH 中使 StudentsBean.class 有效，并且尝试访问上面的 JSP。这将产生以下结果：

<pre class="result notranslate">
Student First Name: Zara 

Student Last Name: Ali 

Student Age: 10 
</pre>
