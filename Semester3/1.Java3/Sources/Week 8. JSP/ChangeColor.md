## Functions.java
```java
package test;

public class Functions {

	public String getRandomColor() {
		String color = "";
		for (int i = 0; i < 3; i++) {
			String sub = Integer.toHexString((int) Math.floor(Math.random() * 256));
			color += (sub.length() == 1) ? "0" + sub : sub;
		}
		return "#" + color;
	}
}
```

## Exercise8-2.jsp
```jsp
<%@ page import="test.Functions"%>
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<%!Functions f = new Functions();%>
	<%
		for (int i = 0; i < 10; i++) {
	%>
	<h1 style='color:<%=f.getRandomColor()%>'>Hello World</h1>
	<%
		}
	%>
</body>
</html>
```