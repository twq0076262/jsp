# JSTL SQL < sql:setDataSource > 标签

`<sql:setDataSource>` 标签设置了数据源配置变量或将数据源信息保存到一个指定范围的变量中，该变量可用作为其他 JSTL 数据库操作的输入。

## 属性：

`<sql:setDataSource>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>driver</td><td>要被注册的 JDBC 驱动程序类名</td><td>否</td><td>无</td></tr>
<tr><td>url</td><td>数据库连接的 JDBC URL</td><td>否</td><td>无</td></tr>
<tr><td>user</td><td>数据库用户名</td><td>否</td><td>无</td></tr>
<tr><td>password</td><td>数据库密码</td><td>否</td><td>无</td></tr>
<tr><td>password</td><td>数据库密码</td><td>否</td><td>无</td></tr>
<tr><td>dataSource</td><td>预先准备的数据库</td><td>否</td><td>无</td></tr>
<tr><td>var</td><td>展示数据库的变量名</td><td>否</td><td>设置默认</td></tr>
<tr><td>scope</td><td>展示数据库的变量范围</td><td>否</td><td>页面</td></tr>
</table>

## 实例：

对你的 MySQL 数据库设置考虑下述信息：

- 我们使用的是 JDBC MySQL 驱动。

- 我们将要连接到本地计算机的 TEST 数据库中。

- 我们将使用 user_id 和密码来访问 TEST 数据库。

所有上述参数会随着你的 MySQL 或任何其他数据库设置而变化。记住上述参数，下面是使用 setDataSource 标签的一个简单的例子：

<pre class="prettyprint notranslate">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql"%&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;JSTL sql:setDataSource Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
 
&lt;sql:setDataSource var="snapshot" driver="com.mysql.jdbc.Driver"
     url="jdbc:mysql://localhost/TEST"
     user="user_id"  password="mypassword"/&gt;

&lt;sql:query dataSource="${snapshot}" sql="..." var="result" /&gt;
 
&lt;/body&gt;
&lt;/html&gt;
</pre>

使用后续的 SQL 标签 < sql:setDataSource > 开始。