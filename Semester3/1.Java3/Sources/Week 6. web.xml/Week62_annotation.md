## web.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="http://xmlns.jcp.org/xml/ns/javaee"
	xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
	id="WebApp_ID" version="3.1">
	<display-name>Week62</display-name>
	<welcome-file-list>
		<welcome-file>index.html</welcome-file>
		<welcome-file>AnnotationTest</welcome-file>
		<welcome-file>index.htm</welcome-file>
		<welcome-file>index.jsp</welcome-file>
		<welcome-file>default.html</welcome-file>
		<welcome-file>default.htm</welcome-file>
		<welcome-file>default.jsp</welcome-file>
	</welcome-file-list>
	<error-page>
		<error-code>404</error-code>
		<location>/pageNotFound.html</location>
	</error-page>

</web-app>
```

## index.html
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	Hello, this is welcome page
</body>
</html>
```

## pageNotFound.html
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<h1>Sorry, we're home right now.  Please leave a message after the beep.</h1>
</body>
</html>
```

## AnnotationTest.java
```java
package sheridan;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

//@WebServlet("/AnnotationTest")
//@WebServlet("/SayHello")
//@WebServlet({ "/AnnotationTest", "/SayHello" })
@WebServlet(name = "ThisIsTheServletNameNotTheURL", description = "This is our servlet description", urlPatterns = {
		"/AnnotationTest", "/SayHello" }, asyncSupported = false)

public class AnnotationTest extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public AnnotationTest() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		try {
			out.write("<h1>Helloooooooooo!</h1>");
		} finally {
			out.close();
		}
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
	}

}
```

## AnnotationTest2.java
```java
package sheridan;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebInitParam;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(asyncSupported = true, description = "This is the second description", urlPatterns = { "/AnnotationTest2",
		"/Test2" }, initParams = {
				@WebInitParam(name = "check", value = "Check 1.. Check 2..", description = "an init parameter for this servlet we can check") })
public class AnnotationTest2 extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public AnnotationTest2() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		String test = getInitParameter("check");

		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		try {
			out.write("<h1>" + test + "</h1>");
		} finally {
			out.close();
		}

	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
	}

}
```

## HelloClientServlet.java
```java
package sheridan;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/HelloClientServlet")
public class HelloClientServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public HelloClientServlet() {
		super();
	}

	protected void doGet(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {
		res.setContentType("text/html");
		PrintWriter out = res.getWriter();
		out.println("<HTML><HEAD><TITLE>Hello World!</TITLE>" + "</HEAD><BODY>Hello World!</BODY></HTML>");
		
		out.println(getServletInfo());
		out.close();
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}

	public String getServletInfo() {
		return "Your first Hello Servlet!";
	}

}
```
