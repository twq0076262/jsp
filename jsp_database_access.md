# 访问数据库 

该教材假定你已经完全理解了 JDBC 应用程序的工作原理。在通过 JSP 访问数据库之前，确保你的数据库有适合的 JDBC 环境设置。 

对于如何用 JDBC 和环境设置访问数据库的更多细节，你可以阅读我们的 [JDBC Tutorial](http://www.tutorialspoint.com/jdbc/index.htm)。 

为了开始基本的概念，我们先创建简单的表和新的记录在该表中，如下所示： 

## 创建表： 

为了在 EMP 数据库中创建 **Employees** 表，用下面的步骤：

### 步骤1： 

打开一个**命令提示符**并且改变安装路径，如下所示：

``` 
C:\>
C:\>cd Program Files\MySQL\bin
C:\Program Files\MySQL\bin>
```

### 步骤2： 

登陆数据库，如下所示：

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

##创建数据记录： 

最后你在 Employee 表中创建一些记录，如下所示：

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

## 查询操作： 

下面的例子显示了我们如何用 JSTL 在 JSP 程序中执行 SQL 查询语句：

<pre class="prettyprint notranslate tryit">
&lt;%@ page import="java.io.*,java.util.*,java.sql.*"%&gt;
&lt;%@ page import="javax.servlet.http.*,javax.servlet.*" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql"%&gt;
 
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;SELECT Operation&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
 
&lt;sql:setDataSource var="snapshot" driver="com.mysql.jdbc.Driver"
     url="jdbc:mysql://localhost/TEST"
     user="root"  password="pass123"/&gt;
 
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

现在尝试访问上述的 JSP 页面，显示的结果如下所示：

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
</table>


## 插入操作： 

下面的例子显示了我们如何用 JSTL 在 JSP 程序中执行 SQL 插入语句：

<pre class="prettyprint notranslate tryit">
&lt;%@ page import="java.io.*,java.util.*,java.sql.*"%&gt;
&lt;%@ page import="javax.servlet.http.*,javax.servlet.*" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql"%&gt;
 
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;JINSERT Operation&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
 
&lt;sql:setDataSource var="snapshot" driver="com.mysql.jdbc.Driver"
     url="jdbc:mysql://localhost/TEST"
     user="root"  password="pass123"/&gt;


&lt;sql:update dataSource="${snapshot}" var="result"&gt;
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


现在尝试访问上述的 JSP 页面，显示的结果如下所示：

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
<td>Nuha</td>
<td>Ali</td>
<td>2</td>
</tr>
</table>


## 删除操作： 

下面的例子显示了我们如何用 JSTL 在 JSP 程序中执行 SQL 删除语句：

<pre class="prettyprint notranslate tryit">
&lt;%@ page import="java.io.*,java.util.*,java.sql.*"%&gt;
&lt;%@ page import="javax.servlet.http.*,javax.servlet.*" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql"%&gt;
 
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;DELETE Operation&lt;/title&gt;
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


现在尝试访问上述的 JSP 页面，显示的结果如下所示：

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


## 更新操作： 

下面的例子显示了我们如何用 JSTL 在 JSP 程序中执行 SQL 更新语句：

<pre class="prettyprint notranslate tryit">
&lt;%@ page import="java.io.*,java.util.*,java.sql.*"%&gt;
&lt;%@ page import="javax.servlet.http.*,javax.servlet.*" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql"%&gt;
 
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;DELETE Operation&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
 
&lt;sql:setDataSource var="snapshot" driver="com.mysql.jdbc.Driver"
     url="jdbc:mysql://localhost/TEST"
     user="root"  password="pass123"/&gt;
 
&lt;c:set var="empId" value="102"/&gt;
 
&lt;sql:update dataSource="${snapshot}" var="count"&gt;
  UPDATE Employees SET last = 'Ali'
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


现在尝试访问上述的 JSP 页面，显示的结果如下所示：

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
<td>Ali</td>
<td>30</td>
</tr>
</table>

