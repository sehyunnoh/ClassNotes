## HelloWorld.jsp
```jsp
<%@ page import="java.util.*" language="java"
	contentType="text/html; charset=ISO-8859-1" pageEncoding="ISO-8859-1"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<% final boolean debug = true; %>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<h1>Hello World from JSP!!!</h1>
	<hr />
	<% out.print("Hello World from JSP Scriptlet!!!"); %>
	<hr />
	<% out.print(new Date()); %>
	<hr />
	<% System.out.println("This is a console test."); %>
	<% for (int i = 1; i <= 6; i++) { %>
	<h<% out.print(i); %>> Big to Small </h<% out.print(i); %>>
	<% } %>
	<% if (debug) { %>
	<span style="color: red;">This page is in debugging mode.. print
		info accordingly.</span>
	<% } %>
	<form method="post" action="Controller">
		Model Number:<input type="text" name="modelNum" /><br /> Serial
		Number:<input type="text" name="serialNum" /><br /> <input
			type="submit" value="Go!" />
	</form>
</body>
</html>
```

## Controller.java
```java
package sheridan;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/Controller")
public class Controller extends HttpServlet {
    public Controller() {
    }
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	}
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		String modelNum = request.getParameter("modelNum");
		String serialNum = request.getParameter("serialNum");
		request.setAttribute("model", modelNum);
		request.setAttribute("serial", serialNum);
		request.setAttribute("warranty", "verified");

		getServletContext().getRequestDispatcher("/Output.jsp").forward(request, response);
	}
}
```

## Output.jsp
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
<title>Insert title here</title>
</head>
<body>

	<h1>Welcome to Sam's Stereo's!</h1>
	
	Your model 
	<% out.print(request.getAttribute("model")); %> and serial
	<% out.print(request.getAttribute("serial")); %> stereo is still under warranty:
	
	<% if (request.getAttribute("warranty").equals("verified")) {
		out.print("Yes!");
	} else {
		out.print("Nope, sorry.");
	} %>
</body>
</html>
```