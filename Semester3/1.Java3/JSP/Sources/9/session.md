## index.jsp
```jsp
<form action="welcome.jsp">
    <input type="text" name="uname">
    <input type="submit" value="go"><br>
</form>
```

## welcome.jsp
```jsp
<body>
	<%
		String name = request.getParameter("uname");
		out.print("Welcome "+name);
		session.setAttribute("user", name);
	%>
	<a href="second.jsp">second jsp page</a>
</body>
```

## second.jsp
```jsp
<body>
	<%
	String name=(String)session.getAttribute("user");
	out.print("Hello "+name);
	%>
</body>
```