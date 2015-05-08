# JSTL Core < fmt:formatDate > 标签

`<fmt:formatDate>` 标签用于以多种方式格式化日期。

## 属性：

`<fmt:formatDate>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>value</td><td>显示的日期值</td><td>是</td><td>无</td></tr>
<tr><td>type</td><td>日期、时间或两者</td><td>否</td><td>日期</td></tr>
<tr><td>dateStyle</td><td>FULL, LONG, MEDIUM, SHORT, 或默认</td><td>否</td><td>默认</td></tr>
<tr><td>timeStyle</td><td>FULL, LONG, MEDIUM, SHORT, 或默认</td><td>否</td><td>默认</td></tr>
<tr><td>pattern</td><td>自定义格式化模式</td><td>否</td><td>无</td></tr>
<tr><td>timeZone</td><td>显示的日期时区</td><td>否</td><td>默认的时区</td></tr>
<tr><td>var</td><td>存储格式化日期的变量名</td><td>否</td><td>页面输出</td></tr>
<tr><td>scope</td><td>存储格式化日期的变量范围</td><td>否</td><td>页面</td></tr>
</table>

pattern 属性指定了更精确地日期处理：

<table class="table table-bordered">
<tr><th style="width:15%">代码</th><th>目的 </th><th>示例</th></tr>
<tr><td><p>G</p></td><td><p>时代指示器</p></td><td><p>AD</p></td></tr>
<tr><td><p>y</p></td><td><p>年</p></td><td><p>2002</p></td></tr>
<tr><td><p>M</p></td><td><p>月</p></td><td><p>April &amp; 04</p></td></tr>
<tr><td><p>d</p></td><td><p>一个月中的某一天</p></td><td><p>20</p></td></tr>
<tr><td><p>h</p></td><td><p>时间(12-hour time)</p></td><td><p>12</p></td></tr>
<tr><td><p>H</p></td><td><p>时间(24-hour time)</p></td><td><p>0</p></td></tr>
<tr><td><p>m</p></td><td><p>分钟</p></td><td><p>45</p></td></tr>
<tr><td><p>s</p></td><td><p>秒</p></td><td><p>52</p></td></tr>
<tr><td><p>S</p></td><td><p>毫秒</p></td><td><p>970</p></td></tr>
<tr><td><p>E</p></td><td><p>一周中的某一天</p></td><td><p>Tuesday</p></td></tr>
<tr><td><p>D</p></td><td><p>一年中的某一天</p></td><td><p>180</p></td></tr>
<tr><td><p>F</p></td><td><p>一个月中的某一周的某一天</p></td><td><p>2 (2nd Wed in month)</p></td></tr>
<tr><td><p>w</p></td><td><p>一年中的某一周</p></td><td><p>27</p></td></tr>
<tr><td><p>W</p></td><td><p>一个月中的某一周</p></td><td><p>2</p></td></tr>
<tr><td><p>a</p></td><td><p>a.m./p.m. 显示器</p></td><td><p>PM</p></td></tr>
<tr><td><p>k</p></td><td><p>时间(12-hour time)</p></td><td><p>24</p></td></tr>
<tr><td><p>K</p></td><td><p>时间(24-hour time)</p></td><td><p>0</p></td></tr>
<tr><td><p>z</p></td><td><p>时区</p></td><td><p>Central Standard Time</p></td></tr>
<tr><td><p>'</p></td><td>&nbsp;</td><td><p>文本消逝</p></td></tr>
<tr><td><p>''</p></td><td>&nbsp;</td><td><p>单引号</p></td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %&gt;
&lt;%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %&gt;

&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;JSTL fmt:dateNumber Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;h3&gt;Number Format:&lt;/h3&gt;
&lt;c:set var="now" value="&lt;%=new java.util.Date()%&gt;" /&gt;

&lt;p&gt;Formatted Date (1): &lt;fmt:formatDate type="time" 
            value="${now}" /&gt;&lt;/p&gt;
&lt;p&gt;Formatted Date (2): &lt;fmt:formatDate type="date" 
            value="${now}" /&gt;&lt;/p&gt;
&lt;p&gt;Formatted Date (3): &lt;fmt:formatDate type="both" 
            value="${now}" /&gt;&lt;/p&gt;
&lt;p&gt;Formatted Date (4): &lt;fmt:formatDate type="both" 
            dateStyle="short" timeStyle="short" 
            value="${now}" /&gt;&lt;/p&gt;
&lt;p&gt;Formatted Date (5): &lt;fmt:formatDate type="both" 
            dateStyle="medium" timeStyle="medium" 
            value="${now}" /&gt;&lt;/p&gt;
&lt;p&gt;Formatted Date (6): &lt;fmt:formatDate type="both" 
            dateStyle="long" timeStyle="long" 
            value="${now}" /&gt;&lt;/p&gt;
&lt;p&gt;Formatted Date (7): &lt;fmt:formatDate pattern="yyyy-MM-dd" 
            value="${now}" /&gt;&lt;/p&gt;

&lt;/body&gt;
&lt;/html&gt;
</pre>

这将会产生如下所示的结果：

<pre class="result notranslate">
<h3>Date Format:</h3>
<p>Formatted Date (1): 14:27:18</p>
<p>Formatted Date (2): 23-Sep-2010</p>
<p>Formatted Date (3): 23-Sep-2010 14:27:18</p>
<p>Formatted Date (4): 23/09/10 14:27</p>
<p>Formatted Date (5): 23-Sep-2010 14:27:18</p>
<p>Formatted Date (6): 23 September 2010 14:27:18 GST</p>
<p>Formatted Date (7): 2010-09-23</p>
</pre>
