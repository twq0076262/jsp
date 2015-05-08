# JSTL Core < fmt:formatNumber > 标签

< fmt:formatNumber > 标签用于格式化数字，百分比和货币。

## 属性：

< fmt:formatNumber > 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>value</td><td>显示的数值</td><td>是</td><td>无</td></tr>
<tr><td>type</td><td>数值、货币或百分比</td><td>否</td><td>数值</td></tr>
<tr><td>pattern</td><td>为输出指定一个自定义格式模式</td><td>否</td><td>无</td></tr>
<tr><td>currencyCode</td><td>Currency 代码 (for type="currency")</td><td>否</td><td>来自默认语言环境</td></tr>
<tr><td>currencySymbol</td><td>Currency 符号 (for type="currency")</td><td>否</td><td>来自默认语言环境</td></tr>
<tr><td>groupingUsed</td><td>是否将数值分组 (TRUE or FALSE)</td><td>否</td><td>true</td></tr>
<tr><td>maxIntegerDigits</td><td>输出的整数位数的最大值</td><td>否</td><td>无</td></tr>
<tr><td>minIntegerDigits</td><td>输出的整数位数的最小值</td><td>否</td><td>无</td></tr>
<tr><td>maxFractionDigits</td><td>输出的小数位数的最大值</td><td>否</td><td>无</td></tr>
<tr><td>minFractionDigits</td><td>输出的小数位数的最小值</td><td>否</td><td>无</td></tr>
<tr><td>var</td><td>存储格式化数字的变量名</td><td>否</td><td>页面输出</td></tr>
<tr><td>scope</td><td>存储格式化数字的变量范围</td><td>否</td><td>页面</td></tr>
</table>

- 如果 type 属性是百分比或数字，那么你可以使用一些数字-格式化属性。maxIntegerDigits 和 minIntegerDigits 属性允许你指定数字的非小数部分的大小。如果实际数字超过了 maxIntegerDigits，那么数字就会被截断。

- 属性同样允许你确定使用多少为小数。minFractionalDigits 和 maxFractionalDigits 属性允许你指定小数位数。如果数字超过了小数位数的最大值，那么数字就会被截断。

- 分组可以用来在成千上万组之间插入逗号。通过将 groupingIsUsed 属性设置为真或假来指定分组。当分组与 minIntegerDigits 一起使用时，必须多加小心来得到你预想的结果。

- 你可能会选择使用 pattern 属性。该属性可以包含特殊字符，指定你有多喜欢编码的数字。下表展示了这些代码。

<table class="table table-bordered">
<tr><th style="width:15%">Symbol</th><th>Description </th></tr>
<tr><td><p>0</p></td><td><p>代表了一个数字。</p></td></tr>
<tr><td><p>E</p></td><td><p>代表了指数形式。</p></td></tr>
<tr><td><p>#</p></td><td><p>代表一个数字；显示 0 为缺席。</p></td></tr>
<tr><td><p>.</p></td><td><p>作为十进制分隔符的一个占位符。</p></td></tr>
<tr><td><p>,</p></td><td><p>作为分组分隔符的一个占位符。</p></td></tr>
<tr><td><p>;</p></td><td><p>分隔形式</p></td></tr>
<tr><td><p>-</p></td><td><p>作为默认的负数前缀。</p></td></tr>
<tr><td><p>%</p></td><td><p>乘以 100 并作为百分比显示。</p></td></tr>
<tr><td><p>?</p></td><td><p>乘以 1000 并作为千分比显示。</p></td></tr>
<tr><td><p>¤</p></td><td><p>代表了货币符号； 被动态的货币符号取代。</p></td></tr>
<tr><td><p>X</p></td><td><p>表明任何其他可以用作前缀或后缀的字符。</p></td></tr>
<tr><td><p>'</p></td><td><p>用于在前缀或后缀中引用特殊字符。</p></td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %&gt;
&lt;%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %&gt;

&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;JSTL fmt:formatNumber Tag&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;h3&gt;Number Format:&lt;/h3&gt;
&lt;c:set var="balance" value="120000.2309" /&gt;
&lt;p&gt;Formatted Number (1): &lt;fmt:formatNumber value="${balance}" 
            type="currency"/&gt;&lt;/p&gt;
&lt;p&gt;Formatted Number (2): &lt;fmt:formatNumber type="number" 
            maxIntegerDigits="3" value="${balance}" /&gt;&lt;/p&gt;
&lt;p&gt;Formatted Number (3): &lt;fmt:formatNumber type="number" 
            maxFractionDigits="3" value="${balance}" /&gt;&lt;/p&gt;
&lt;p&gt;Formatted Number (4): &lt;fmt:formatNumber type="number" 
            groupingUsed="false" value="${balance}" /&gt;&lt;/p&gt;
&lt;p&gt;Formatted Number (5): &lt;fmt:formatNumber type="percent" 
            maxIntegerDigits="3" value="${balance}" /&gt;&lt;/p&gt;
&lt;p&gt;Formatted Number (6): &lt;fmt:formatNumber type="percent" 
            minFractionDigits="10" value="${balance}" /&gt;&lt;/p&gt;
&lt;p&gt;Formatted Number (7): &lt;fmt:formatNumber type="percent" 
            maxIntegerDigits="3" value="${balance}" /&gt;&lt;/p&gt;
&lt;p&gt;Formatted Number (8): &lt;fmt:formatNumber type="number" 
            pattern="###.###E0" value="${balance}" /&gt;&lt;/p&gt;
&lt;p&gt;Currency in USA :
&lt;fmt:setLocale value="en_US"/&gt;
&lt;fmt:formatNumber value="${balance}" type="currency"/&gt;&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

这将会产生如下所示结果：

<pre class="result notranslate">
<h3>Number Format:</h3>
<p>Formatted Number (1): £120,000.23</p>
<p>Formatted Number (2): 000.231</p>
<p>Formatted Number (3): 120,000.231</p>
<p>Formatted Number (4): 120000.231</p>
<p>Formatted Number (5): 023%</p>
<p>Formatted Number (6): 12,000,023.0900000000%</p>
<p>Formatted Number (7): 023%</p>
<p>Formatted Number (8): 120E3</p>
<p>Currency in USA : $120,000.23</p>
</pre>
