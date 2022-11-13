## EL表达式

Expression Language 表达式语言，用于简化JSP页面的Java代码

主要功能：获取数据

语法：${expression}

```java
Brand brand = new Brand(1,"三只松鼠")
//存储到request域中
request.setAttribute("brand",brand);
```

```jsp
<%@ page isELIgnored="false" %>><!--不忽略el表达式-->
<body>
    ${brand}  <!--获取域存储的key为brand的数据-->
    <!--
		{1,三只松鼠}
	-->
</body>
```

JavaWeb中的四大域对象

1.page：当前页面有效

2.request：当前请求有效

3.session：当前会话有效

4.application：当前应用有效

el表达式会从这4个域依次寻找，直到找到为止

## JSTL标签

JSP标准标签库(Jsp Standarded Tag Library),使用标签取代JSP页面上的Java代码

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %><!--引用核心标签库-->

标签	描述
<c:out>				用于在JSP中显示数据，就像<%= ... >
<c:set>				用于保存数据
<c:remove>			用于删除数据
<c:catch>			用来处理产生错误的异常状况，并且将错误信息储存起来
<c:if>				与我们在一般程序中用的if一样
<c:choose>			本身只当做<c:when>和<c:otherwise>的父标签
<c:when>			<c:choose>的子标签，用来判断条件是否成立
<c:otherwise>		<c:choose>的子标签，接在<c:when>标签后，当<c:when>标签判断为false时被执行
<c:import>			检索一个绝对或相对 URL，然后将其内容暴露给页面
<c:forEach>			基础迭代标签，接受多种集合类型
<c:forTokens>		根据指定的分隔符来分隔内容并迭代输出
<c:param>			用来给包含或重定向的页面传递参数
<c:redirect>		重定向至一个新的URL.
<c:url>				使用可选的查询参数来创造一个URL
```

```xml
<!--用maven 需要导入坐标-->
<!--引入jstl标签  jstl  standard-->
    <dependency>
      <groupId>jstl</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
    </dependency>
    <dependency>
      <groupId>taglibs</groupId>
      <artifactId>standard</artifactId>
      <version>1.1.2</version>
    </dependency>
```

### if标签

<c: if>

属性：test，用于定义条件表达式

定义一个 servlet ，在该 servlet 中向 request 域对象中添加 键是 status ，值为 1 的数据

```java
request.setAttribute("status",1);
```

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page isELIgnored="false" %><!--不忽略el表达式-->
<html>
<head>
    <title>Title</title>
</head>
<body>
    <%-- c:if 完成逻辑判断，替换java if else --%>
    <c:if test="${status ==1}">
        <h1>你好</h1> 
    </c:if>
    <c:if test="${status ==0}">
        <h1>不好</h1>
    </c:if>
</body>
</html>
```

### forEach标签

测试<c: forEach>

用法1：

1. 类似于 Java 中的增强for循环。涉及到的<c: forEach>中的属性如下 
2. items：被遍历的容器 
3. var：遍历产生的临时变量 
4. varStatus：遍历状态对象 

如下代码，是从域对象中获取名为 brands 数据，该数据是一个集合；遍历遍历，并给该集合中的每一个元素起名为 brand ，是 Brand对象。在循环里面使用 EL表达式获取每一个Brand对象的属性值

```jsp
<c:forEach items="${brands}" var="brand">
	<tr align="center">
		<td>${brand.id}</td>
		<td>${brand.brandName}</td>
		<td>${brand.companyName}</td>
		<td>${brand.description}</td>
	</tr>
</c:forEach>
```

用法2

类似于 Java 中的普通for循环。涉及到的<c: forEach>中的属性如下

begin：开始数 

end：结束数 

step：步长

实例代码： 从0循环到10，变量名是 i ，每次自增1

```jsp
<c:forEach begin="0" end="10" step="1" var="i">
		${i}
</c:forEach>
```

