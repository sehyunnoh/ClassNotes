## HelloWorld.jsp
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<h1>
		<%
			out.println("Welcome from first JSP page!");
		%>
	</h1>
	<h2 style='color: blue; background-color: red'>
		<%
			out.println(new java.util.Date());
		%>
	</h2>
	<%
		boolean debug = true;
		if (debug)
			System.out.println("To be directed to the console!");
		int i = 1;
		for (i = 1; i <= 6; i++) {
	%>
	<h <%=i%>> <br>
	Big to small </h<%=i%>>
	<%
		}
	%>
	<%
		final boolean debug1 = true;
		if (debug1) {
	%>
	<span style="color: red;">This page is in debugging mode.. print
		info accordingly.</span>
	<% } %>

</body>
</html>
```