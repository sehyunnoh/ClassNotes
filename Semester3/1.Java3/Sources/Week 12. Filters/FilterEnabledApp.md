## index.html
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<form action="EchoServlet">
		First Name <input type="text" name="fname"> <br>
		<input type="submit" value="Go">
	</form>

</body>
</html>
```

## web.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="http://java.sun.com/xml/ns/javaee"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
	version="3.0">
	<display-name>FilterEnabledApp</display-name>
	<welcome-file-list>
		<welcome-file>index.html</welcome-file>
		<welcome-file>index.htm</welcome-file>
		<welcome-file>index.jsp</welcome-file>
		<welcome-file>default.html</welcome-file>
		<welcome-file>default.htm</welcome-file>
		<welcome-file>default.jsp</welcome-file>
	</welcome-file-list>
	<filter>
		<filter-name>logger</filter-name>
		<filter-class>ca.sheridancollege.filters.Logger</filter-class>
	</filter>
	<filter>
		<filter-name>logger2</filter-name>
		<filter-class>ca.sheridancollege.filters.Logger2</filter-class>
	</filter>
	<filter>
		<filter-name>blocker</filter-name>
		<filter-class>ca.sheridancollege.filters.Blocker</filter-class>
		<init-param>
			<param-name>bTime</param-name>
			<param-value>17</param-value>
		</init-param>
		<init-param>
			<param-name>eTime</param-name>
			<param-value>19</param-value>
		</init-param>
	</filter>

	<filter-mapping>
		<filter-name>logger</filter-name>
		<url-pattern>/EchoServlet</url-pattern>
	</filter-mapping>
	<filter-mapping>
		<filter-name>logger2</filter-name>
		<url-pattern>/EchoServlet</url-pattern>
	</filter-mapping>
	<filter-mapping>
		<filter-name>blocker</filter-name>
		<url-pattern>/Servlet1</url-pattern>
	</filter-mapping>
</web-app>
```

## Logger.java
```java
package ca.sheridancollege.filters;

import java.io.IOException;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;
import javax.servlet.http.HttpServletResponse;

@WebFilter("/Logger")
public class Logger implements Filter {
	private FilterConfig fc;

    public Logger() {
    }

	public void destroy() {
	}

	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
		HttpServletResponse myResponse = (HttpServletResponse) response;
		myResponse.getWriter().append("<div style='color:green'>" + 
		          "Hello " + request.getParameter("fname") + " a message from the filter!" + "</div>");
		chain.doFilter(request, response);
	}

	public void init(FilterConfig fConfig) throws ServletException {
		this.fc = fConfig;
	}

}
```

## Logger2.java
```java
package ca.sheridancollege.filters;

import java.io.IOException;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;
import javax.servlet.http.HttpServletResponse;

@WebFilter("/Logger2")
public class Logger2 implements Filter {
	FilterConfig fc;

    public Logger2() {
    }

	public void destroy() {
	}

	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
		HttpServletResponse myResponse = (HttpServletResponse) response;
		myResponse.getWriter().append("<div style='color:red'>" + 
		          "Hello " + request.getParameter("fname") + " a message from the filter2!" + "</div>");
		chain.doFilter(request, response);
	}

	public void init(FilterConfig fConfig) throws ServletException {
		this.fc = fConfig;
	}

}
```

## Blocker.java
```java
package ca.sheridancollege.filters;

import java.io.IOException;
import java.util.Calendar;
import java.util.Date;

import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;

@WebFilter("/Blocker")
public class Blocker implements Filter {
	FilterConfig fc;

	public Blocker() {
	}

	public void destroy() {
	}

	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
			throws IOException, ServletException {
		int bHour = Integer.parseInt(fc.getInitParameter("bTime"));
		int eHour = Integer.parseInt(fc.getInitParameter("eTime"));
		Calendar c = Calendar.getInstance();
//		int currentHour = c.get(Calendar.HOUR_OF_DAY);
		int currentHour = 18;
		if (currentHour >= bHour && currentHour <= eHour)
			System.out.println("Warning! you are not allowed to access" + "this resource at the current time");
		else
			System.out.println("The server at " + request.getRemoteHost() + " was accessed at " + new Date() + "from "
					+ request.getRemoteAddr());

		chain.doFilter(request, response);
	}

	public void init(FilterConfig fConfig) throws ServletException {
		this.fc = fConfig;
	}

}
```

## EchoServlet.java
```java
package ca.sheridancollege.servlets;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/EchoServlet")
public class EchoServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public EchoServlet() {
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		System.out.println("/EchoServlet");
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}

}
```

## Servlet1.java
```java
package ca.sheridancollege.servlets;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/Servlet1")
public class Servlet1 extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public Servlet1() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.getWriter().append("Served at: ").append(request.getContextPath());
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}

}
```
