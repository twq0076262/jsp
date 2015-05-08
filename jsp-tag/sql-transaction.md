# JSTL SQL < sql:transaction > 标签

`<sql:transaction>` 标签用于将 `<sql:query>` 和 `<sql:update>` 标签分组到事物中。你可以在 `<sql:transaction>` 标签中放入和语句一样多的 `<sql:query>` 和 `<sql:update>` 标签，使它们成为单独的事物。

如果任何嵌套操作抛出一个异常，它确保由嵌套操作执行的数据库修改要么提交要么回滚。

## 属性：

`<sql:transaction>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>dataSource</td><td>要使用的数据库连接 (覆盖默认值)</td><td>否</td><td>默认数据库</td></tr>
<tr><td>isolation</td><td>事务隔离 (READ_COMMITTED，READ_UNCOMMITTED，EPEATABLE_READ，或 SERIALIZABLE)</td><td>否</td><td>数据库的默认值</td></tr>
</table>

## 实例：

从基本概念开始，在 TEST 数据库中创建一个简单的 **Students** 表，并在表中创建几条记录，如下所示：

### 步骤1：

打开 **Command Prompt** 并改变为安装目录，如下所示：

``` 
C:\>
C:\>cd Program Files\MySQL\bin
C:\Program Files\MySQL\bin>
```

### 步骤2：

登录数据库，如下所示：

``` 
C:\Program Files\MySQL\bin>mysql -u root -p
Enter password: ********
mysql>
``` 

### 步骤3：

在 **TEST** 数据库中创建 **Student** 表：

``` 
mysql> use TEST;
mysql> create table Students
    (
     id int not null,
     first varchar (255),
     last varchar (255),
     dob date
    );
Query OK, 0 rows affected (0.08 sec)
mysql>
```

## 创建数据记录


最后在 Student 表中创建几条记录，如下所示：

``` 
mysql> INSERT INTO Students 
          VALUES (100, 'Zara', 'Ali', '2002/05/16');
Query OK, 1 row affected (0.05 sec)
mysql> INSERT INTO Students 
          VALUES (101, 'Mahnaz', 'Fatma', '1978/11/28');
Query OK, 1 row affected (0.00 sec)
mysql> INSERT INTO Students 
          VALUES (102, 'Zaid', 'Khan', '1980/10/10');
Query OK, 1 row affected (0.00 sec)
mysql> INSERT INTO Students 
          VALUES (103, 'Sumit', 'Mittal', '1971/05/08');
Query OK, 1 row affected (0.00 sec)
mysql>
```

现在编写 JSP，使用 `<sql:update>` 和 `<sql:transaction>` 标签来执行 SQL UPDATE 语句。在这里 `<sql:transaction>` 标签内的代码要么被完全执行，要么一点也不执行：

<pre class="prettyprint notranslate tryit">
&lt;%@ page import="java.io.*,java.util.*,java.sql.*"%&gt;
&lt;%@ page import="javax.servlet.http.*,javax.servlet.*"%&gt;
&lt;%@ page import="java.util.Date,java.text.*" %&gt;

&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql"%&gt;
 
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;JSTL sql:transaction Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
 
&lt;sql:setDataSource var="snapshot" driver="com.mysql.jdbc.Driver"
     url="jdbc:mysql://localhost/TEST"
     user="root"  password="cohondob"/&gt;

&lt;%
Date DoB = new Date("2001/12/16");
int studentId = 100;
%&gt;

&lt;sql:transaction dataSource="${snapshot}"&gt;
   &lt;sql:update var="count"&gt;
      UPDATE Students SET last = 'Ali' WHERE Id = 102
   &lt;/sql:update&gt;
   &lt;sql:update var="count"&gt;
      UPDATE Students SET last = 'Shah' WHERE Id = 103
   &lt;/sql:update&gt;
   &lt;sql:update var="count"&gt;
     INSERT INTO Students 
     VALUES (104,'Nuha', 'Ali', '2010/05/26');
   &lt;/sql:update&gt;
&lt;/sql:transaction&gt;

&lt;sql:query dataSource="${snapshot}" var="result"&gt;
   SELECT * from Students;
&lt;/sql:query&gt;
 
&lt;table border="1" width="100%"&gt;
&lt;tr&gt;
&lt;th&gt;Emp ID&lt;/th&gt;
&lt;th&gt;First Name&lt;/th&gt;
&lt;th&gt;Last Name&lt;/th&gt;
&lt;th&gt;DoB&lt;/th&gt;
&lt;/tr&gt;
&lt;c:forEach var="row" items="${result.rows}"&gt;
&lt;tr&gt;
&lt;td&gt;&lt;c:out value="${row.id}"/&gt;&lt;/td&gt;
&lt;td&gt;&lt;c:out value="${row.first}"/&gt;&lt;/td&gt;
&lt;td&gt;&lt;c:out value="${row.last}"/&gt;&lt;/td&gt;
&lt;td&gt;&lt;c:out value="${row.dob}"/&gt;&lt;/td&gt;
&lt;/tr&gt;
&lt;/c:forEach&gt;
&lt;/table&gt;
 
&lt;/body&gt;
&lt;/html&gt;
</pre>

现在尝试访问上述 JSP，会出现如下所示结果：

<pre class="result notranslate">
<table border="1" width="100%">
<tr>
<th>Emp ID</th>
<th>First Name</th>
<th>Last Name</th>
<th>DoB</th>
</tr>
<tr>
<td>100</td>
<td>Zara</td>
<td>Ali</td>
<td>2001-12-16</td>
</tr>
<tr>
<td>101</td>
<td>Mahnaz</td>
<td>Fatma</td>
<td>1978-11-28</td>
</tr>
<tr>
<td>102</td>
<td>Zaid</td>
<td>Ali</td>
<td>1980-10-10</td>
</tr>
<tr>
<td>103</td>
<td>Sumit</td>
<td>Shah</td>
<td>1971-05-08</td>
</tr>
<tr>
<td>104</td>
<td>Nuha</td>
<td>Ali</td>
<td>2010-05-26</td>
</tr>
</table>
</pre>

