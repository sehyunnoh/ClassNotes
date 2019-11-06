```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="UTF-8"%>
<%@ page import="test.Test"%>

<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<h1>Hello World from JSP!!</h1>
	<%
		out.print("Hello World from JSP Scriptlet!!");
	%>
	<br>
	<%
		out.print(new java.util.Date());
	%>
	<%
		System.out.println("This is a console test.");
	%>
	<%
		for(int i=1; i<= 6; i++){
	%>
	<h<%out.print(i);%>> Big to Small </h<%out.print(i);%>>
	<%
		}
	%>
	<%
		final boolean debug = true;
	%>
	<%
		if(debug){
	%>
	<span style="color: red;">print info</span>
	<%
		}
	%>
	<%-- This is a jsp comment --%>
	<%
		String firstName = "Ol";
			int x = 10;
	%>
	<hr />
	Some HTML
	<hr />
	<%=firstName%>
	<%=x%>
	<%=firstName%>
	<%
		x=x+25;
	%>
	<%
		firstName+=25;
	%>
	<%=firstName%>
	<%!double calculateFahrenheit(double celsius){
		return celsius*9 / 5 + 32;				
	}%>
	<%
	 	int count=0;
	 %>
	The page count is now:
	<%=++count%>
	
	<% Test t = new Test(); %>
	<% t.setNum(10);%>
	<% out.print("result number: "+t.getNum());%>
	
	<% x=1;
		while(x<=3){
			out.println(x + "<br>");
			x++;
		}
	%>

</body>
</html>
```