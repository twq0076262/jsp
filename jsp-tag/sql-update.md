# JSTL SQL < sql:update > 标签

`<sql:update>` 标签执行不返回数据的 SQL 语句，例如 SQL INSERT，UPDATE，或 DELETE 语句。

## 属性：

`<sql:update>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>sql</td><td>要执行的 SQL 语句 (应不返回 ResultSet)</td><td>否</td><td>Body</td></tr>
<tr><td>dataSource</td><td>要使用的数据库连接 (覆盖默认值)</td><td>否</td><td>默认数据库</td></tr>
<tr><td>var</td><td>存储受影响行数的变量名</td><td>否</td><td>无</td></tr>
<tr><td>scope</td><td>存储受影响行数的变量范围</td><td>否</td><td>页面</td></tr>
</table>

## 实例：

从基本概念开始，在 TEST 数据库中创建一个简单的 **Employees** 表，并在表中创建如下所示的几行记录：

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

最后在 Employee 表中创建如下所示的几条记录：

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

现在编写 JSP，使用 `<sql:update>` 标签来执行 SQL INSERT 语句，从而在表中创建一条记录，如下所示：

<pre class="prettyprint notranslate">
&lt;%@ page import="java.io.*,java.util.*,java.sql.*"%&gt;
&lt;%@ page import="javax.servlet.http.*,javax.servlet.*" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql"%&gt;

&lt;html&gt;
&lt;head&gt;
&lt;title&gt;JSTL sql:update Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
 
&lt;sql:setDataSource var="snapshot" driver="com.mysql.jdbc.Driver"
     url="jdbc:mysql://localhost/TEST"
     user="root"  password="pass123"/&gt;

&lt;sql:update dataSource="${snapshot}" var="count"&gt;
   INSERT INTO Employees VALUES (104, 2, 'Nuha', 'Ali');
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

现在尝试访问上述 JSP，将显示如下所示结果：

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
<tr>
<td>103</td>
<td>Sumit</td>
<td>Mittal</td>
<td>28</td>
</tr>
<tr>
<td>104</td>
<td>Nula</td>
<td>Ali</td>
<td>2</td>
</tr>
</table>
</pre>

同样的方式，你可以在相同的表中尝试 SQL UPDATE 和 DELETE 语句。
