# JSTL SQL < sql:param > 标签

< sql:param > 标签用于 <sql:query> 和 <sql:update> 标签的嵌套操作，来为一个值的占位符提供值。如果提供了一个空值，那么占位符就会被设置为 SQL NULL。

## 属性：

< sql:param > 标签具有如下属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>value</td><td>要设置的参数值</td><td>否</td><td>Body</td></tr>
</table>

## 实例：

从基本概念开始，在 TEST 数据库中创建一个简单的 **Employees** 表，并创建几条记录，如下所示：

### 步骤1：

打开 **Command Prompt**，并改变为安装目录，如下所示：

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

在 **TEST** 数据库中创建 **Employee** 表，如下所示：

``` 
mysql> use TEST;
mysql> create table Employees
    (
     id int not null,
     age int not null,
     first varchar (255),
     last varchar (255)
    );
Query OK, 0 rows affected (0.08 sec)
mysql>
```

## 创建数据记录

最后在 Employee 表中创建几条记录，如下所示：

``` 
mysql> INSERT INTO Employees VALUES (100, 18, 'Zara', 'Ali');
Query OK, 1 row affected (0.05 sec)
mysql> INSERT INTO Employees VALUES (101, 25, 'Mahnaz', 'Fatma');
Query OK, 1 row affected (0.00 sec)
mysql> INSERT INTO Employees VALUES (102, 30, 'Zaid', 'Khan');
Query OK, 1 row affected (0.00 sec)
mysql> INSERT INTO Employees VALUES (103, 28, 'Sumit', 'Mittal');
Query OK, 1 row affected (0.00 sec)
mysql>
```

现在编写 JSP，使用 <sql:update> 标签来执行 SQL DELETE 语句来从表中删除一条 id=103 的记录，如下所示：

<pre class="prettyprint notranslate tryit">
&lt;%@ page import="java.io.*,java.util.*,java.sql.*"%&gt;
&lt;%@ page import="javax.servlet.http.*,javax.servlet.*" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql"%&gt;

&lt;html&gt;
&lt;head&gt;
&lt;title&gt;JSTL sql:param Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
 
&lt;sql:setDataSource var="snapshot" driver="com.mysql.jdbc.Driver"
     url="jdbc:mysql://localhost/TEST"
     user="root"  password="pass123"/&gt;

&lt;c:set var="empId" value="103"/&gt;

&lt;sql:update dataSource="${snapshot}" var="count"&gt;
  DELETE FROM Employees WHERE Id = ?
  &lt;sql:param value="${empId}" /&gt;
&lt;/sql:update&gt;

&lt;sql:query dataSource="${snapshot}" var="result"&gt;
   SELECT * from Employees;
&lt;/sql:query&gt;
 
&lt;table border="1" width="100%"&gt;
&lt;tr&gt;
&lt;th&gt;Emp ID&lt;/th&gt;
&lt;th&gt;First Name&lt;/th&gt;
&lt;th&gt;Last Name&lt;/th&gt;
&lt;th&gt;Age&lt;/th&gt;
&lt;/tr&gt;
&lt;c:forEach var="row" items="${result.rows}"&gt;
&lt;tr&gt;
&lt;td&gt;&lt;c:out value="${row.id}"/&gt;&lt;/td&gt;
&lt;td&gt;&lt;c:out value="${row.first}"/&gt;&lt;/td&gt;
&lt;td&gt;&lt;c:out value="${row.last}"/&gt;&lt;/td&gt;
&lt;td&gt;&lt;c:out value="${row.age}"/&gt;&lt;/td&gt;
&lt;/tr&gt;
&lt;/c:forEach&gt;
&lt;/table&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

现在尝试访问上述 JSP，会显示如下所示的结果：

<pre class="result notranslate">
<table border="1" width="100%">
<tr>
<th>Emp ID</th>
<th>First Name</th>
<th>Last Name</th>
<th>Age</th>
</tr>
<tr>
<td>100</td>
<td>Zara</td>
<td>Ali</td>
<td>18</td>
</tr>
<tr>
<td>101</td>
<td>Mahnaz</td>
<td>Fatma</td>
<td>25</td>
</tr>
 <tr>
<td>102</td>
<td>Zaid</td>
<td>Khan</td>
<td>30</td>
</tr>
</table>
</pre>

你可以用这里我使用的 DELETE 语句同样的方式尝试 SQL UPDATE 和 SELECT 语句的 < sql:param > 标签