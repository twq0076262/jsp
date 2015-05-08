# JSTL SQL < sql:query > 标签

< sql:query > 标签执行 SQL SELECT 语句并将结果保存到给定范围的变量中。

## 属性：

< sql:query > 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>sql</td><td>要执行的 SQL 命令 (应返回 ResultSet)</td><td>否</td><td>Body</td></tr>
<tr><td>dataSource</td><td>要用的数据库连接 (覆盖默认值)</td><td>否</td><td>默认数据库</td></tr>
<tr><td>maxRows</td><td>存储在变量中的结果的最大值</td><td>否</td><td>不限</td></tr>
<tr><td>startRow</td><td>结果中开始记录的行数</td><td>否</td><td>0</td></tr>
<tr><td>var</td><td>显示数据库的变量名</td><td>否</td><td>设置默认</td></tr>
<tr><td>scope</td><td>显示来自数据库的结果的变量范围</td><td>否</td><td>页面</td></tr>
</table>

## 实例：

从基本概念开始，让我们在 TEST 数据库中创建一个简单的 **Employees** 表，并在表中创建如下所示的几行记录：

### 步骤1：

打开 **Command Prompt** 并改变为如下所示的安装目录：

``` 
C:\>
C:\>cd Program Files\MySQL\bin
C:\Program Files\MySQL\bin>
```

### 步骤2：

按如下所示方法登录数据库

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

最后在 Employee 表中创建几行记录，如下所示：

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

现在让我们编写一个 JSP，使用 <sql:query> 来执行 SQL SELECT 语句，如下所示：

<pre class="prettyprint notranslate tryit">
&lt;%@ page import="java.io.*,java.util.*,java.sql.*"%&gt;
&lt;%@ page import="javax.servlet.http.*,javax.servlet.*" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql"%&gt;

&lt;html&gt;
&lt;head&gt;
&lt;title&gt;JSTL sql:query Tag&lt;/title&gt;
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

现在尝试访问上述 JSP，会出现如下所示结果：

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
</table>
</pre>
