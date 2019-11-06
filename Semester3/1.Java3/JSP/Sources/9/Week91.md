## Student.java

```java
package model;

import java.io.Serializable;

public class Student implements Serializable {

	private int ID;
	private String firstName;
	private String lastName;

	public Student() {
	}

	public int getID() {
		return ID;
	}

	public void setID(int iD) {
		ID = iD;
	}

	public String getFirstName() {
		return firstName;
	}

	public void setFirstName(String firstName) {
		this.firstName = firstName;
	}

	public String getLastName() {
		return lastName;
	}

	public void setLastName(String lastName) {
		this.lastName = lastName;
	}

}
```

## Controller.java

```java
import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import model.Student;

@WebServlet("/Controller")
public class Controller extends HttpServlet {
	Student myStudent;

	public Controller() {
		myStudent = new Student();
		myStudent.setID(12345);
		myStudent.setFirstName("John");
		myStudent.setLastName("Smith");
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.getWriter().append("Served at: ").append(request.getContextPath());
		RequestDispatcher rd = request.getRequestDispatcher("View.jsp");
		request.setAttribute("student", myStudent);
		rd.forward(request, response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}

}
```

## view.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<%@ page import="model.Student"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Display Students Information</title>
</head>
<body>
	<%
		Student std = (Student) request.getAttribute("student");
	%>
	<h1 style="color: blue">
		ID: <%=std.getID()%><br> 
		First Name: <%=std.getFirstName()%><br> 
		Last Name: <% out.print(std.getLastName()); %>
	<hr>
	
	<jsp:useBean id="student" class="model.Student" scope="session"></jsp:useBean>
	<h1 style="color: blue">
		ID: <jsp:getProperty property="ID" name="student" /><br>
		First Name: <jsp:getProperty property="firstName" name="student" /><br>
		Last Name: <jsp:getProperty property="lastName" name="student" />
	<hr>
	
	<h2 style="color: red">
		ID: ${student.ID} <br> 
		First Name: ${student.firstName} <br>
		Last Name: ${student.lastName}
</body>
</html>
```
