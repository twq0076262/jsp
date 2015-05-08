# JSTL Core < fmt:timeZone > 标签

`<fmt:timeZone>` 标签用于指定所有标签主体内用到的时区。

## 属性：

`<fmt:timeZone>` 标签具有如下所示属性：

<table class="table table-bordered">
<tr><th style="width:15%">属性</th><th>描述 </th><th>是否必需</th><th>默认值</th></tr>
<tr><td>value</td><td>应用于主体的时区</td><td>是</td><td>无</td></tr>
</table>

## 实例：

<pre class="prettyprint notranslate tryit">
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;
&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;JSTL fmt:timeZone Tag&lt;/title&gt;
  &lt;/head&gt;

  &lt;body&gt;
    &lt;c:set var="now" value="&lt;%=new java.util.Date()%&gt;" /&gt;
    &lt;table border="1" width="100%"&gt;
      &lt;tr&gt;
        &lt;td width="100%" colspan="2" bgcolor="#0000FF"&gt;
          &lt;p align="center"&gt;
            &lt;b&gt;
              &lt;font color="#FFFFFF" size="4"&gt;Formatting:
              &lt;fmt:formatDate value="${now}" type="both"
              timeStyle="long" dateStyle="long" /&gt;
              &lt;/font&gt;
            &lt;/b&gt;
          &lt;/p&gt;
        &lt;/td&gt;
      &lt;/tr&gt;

      &lt;c:forEach var="zone"
      items="&lt;%=java.util.TimeZone.getAvailableIDs()%&gt;"&gt;
        &lt;tr&gt;
          &lt;td width="51%"&gt;
            &lt;c:out value="${zone}" /&gt;
          &lt;/td&gt;
          &lt;td width="49%"&gt;
            &lt;fmt:timeZone value="${zone}"&gt;
              &lt;fmt:formatDate value="${now}" timeZone="${zn}"
              type="both" /&gt;
            &lt;/fmt:timeZone&gt;
          &lt;/td&gt;
        &lt;/tr&gt;
      &lt;/c:forEach&gt;
    &lt;/table&gt;
  &lt;/body&gt;
&lt;/html&gt;
</pre>

这将产生如下所示结果：

<pre class="result notranslate">
<table border="1"  width="100%">
      <tr>
        <td width="100%" colspan="2" bgcolor="#0000FF">
          <p align="center">
            <b>
              <font color="#FFFFFF" size="2">Formatting:  23 September 2010 15:09:09 GST </font>
            </b>
          </p>
        </td>
      </tr>
      <tr>
          <td width="51%">
            Etc/GMT+12
          </td>
          <td width="49%">
            
              22-Sep-2010 23:09:09
            
          </td>
        </tr>
        <tr>
          <td width="51%">
            Etc/GMT+11
          </td>
          <td width="49%">
            
              23-Sep-2010 00:09:09
            
          </td>
        </tr>
</table>
...........................
</pre>
