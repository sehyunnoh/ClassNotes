## NewEmployee.jsp
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
	<form method="post" action="View.jsp">
		ID: <input type="text" name="id"><br> 
		First Name: <input type="text" name="fname"><br> 
		Last Name: <input
			type="text" name="lname"><br> Salary: <input
			type="number" name="salary"><br> <input type="submit"
			value="Net Pay">
	</form>
</body>
</html>
```

## View.jsp
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Net Pay</title>
</head>
<body>
	<%
		request.setAttribute("sal", Double.parseDouble(request.getParameter("salary")));
	%>
	<h1>Employee Info</h1>
	<h2>${param.id}</h2>
	<br>
	<h2>${param.fname}</h2>
	<br>
	<h2>${param.lname}</h2>
	<br>
	<c:choose>
		<c:when test="${sal < 30000}">
			<h2 style="color: red">Salary = ${sal}</h2>
		</c:when>
		<c:when test="${sal >= 30000 && sal < 50000}">
			<h2 style="color: red">Salary = ${sal- sal*0.18}</h2>
		</c:when>
		<c:when test="${sal >= 50000 && sal < 75000}">
			<h2 style="color: red">Salary = ${sal- sal*0.26}</h2>
		</c:when>
		<c:when test="${sal >= 75000 && sal < 100000}">
			<h2 style="color: red">Salary = ${sal- sal*0.31}</h2>
		</c:when>
		<c:otherwise>
			<h2 style="color: red">Salary = ${sal- sal*0.35}</h2>
		</c:otherwise>
	</c:choose>
</body>
</html>
```