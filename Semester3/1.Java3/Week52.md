## toPost.html
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<form method="post" action="Servlet1">
		<input type="submit" value="Go!" />
	</form>
</body>
</html>
```

## Names.java
```java
package sheridan;

import java.io.Serializable;

public class Names implements Serializable {

	private String firstName;
	private String lastName;

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

	public Names(String firstName, String lastName) {
		this.firstName = firstName;
		this.lastName = lastName;
	}

	public Names() {
	}

}
```

## Servlet1.java
```java
package sheridan;

import java.io.IOException;
import java.io.PrintWriter;

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
		PrintWriter out = response.getWriter();
		out.write("<html><body>");
		out.write("<h1>This is Servlet2 doGet</h1>");
		out.write("</body></html>");

		out.close();

		response.sendRedirect("Servlet2");
		// getServletContext().getRequestDispatcher("/Servlet2").forward(request,
		// response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		Names newName = new Names("Tom", "Cruise");
		request.setAttribute("newName", newName);

		request.getRequestDispatcher("/Servlet2").forward(request, response);
//		 getServletContext().getRequestDispatcher("/Servlet2").forward(request,
//				 response);
//		response.sendRedirect("Servlet2");
	}

}
```

## Servlet2.java
```java
package sheridan;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/Servlet2")
public class Servlet2 extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public Servlet2() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		PrintWriter out = response.getWriter();

		out.write("<html><body>");
		out.write("<h1>This is Servlet2 doGet</h1>");

		Names newName = (Names) request.getAttribute("newName");
		if (newName == null) {
			out.write("No newName attribute here!");
		} else {
			out.write(newName.getFirstName() + " " + newName.getLastName());
		}

		out.write("</body></html>");

		out.close();
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		PrintWriter out = response.getWriter();

		out.write("<html><body>");
		out.write("<h1>This is Servlet2 doPost</h1>");

		Names newName = (Names) request.getAttribute("newName");
		out.write(newName.getFirstName() + " " + newName.getLastName());

		out.write("</body></html>");

		out.close();
	}
}
```