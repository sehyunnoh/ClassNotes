## DataAccess.java
```java

import java.sql.Connection;
import java.sql.Date;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.sql.Time;
import java.util.GregorianCalendar;
import java.util.Scanner;

public class DataAccess {
	private static final String username = "root";
	private static final String password = "";
	private static final String connURL = "jdbc:mysql://localhost:3306/hotsummer";
	private Connection connection = null;

	public DataAccess() {
		try {
			Class.forName("com.mysql.jdbc.Driver");
		} catch (ClassNotFoundException e) {
			System.err.println("ERROR: mysql.com.jdbc.Driver not found.");
		}

	}

	public boolean connect() {
		try {
			connection = DriverManager.getConnection(connURL, username, password);

		} catch (SQLException e) {
			System.err.println("could not connect to the database" + e.getMessage());
			return false;
		}
		return true;
	}

	public ResultSet listProducts() {
		Statement stat = null;
		ResultSet rs = null;
		String sql = "SELECT * FROM course;";
		try {
			stat = connection.createStatement();
			rs = stat.executeQuery(sql);
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		return rs;
	}
}
```

## Servlet 1
```java

import java.io.IOException;
import java.io.PrintWriter;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;

import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/Servlet1")
public class Servlet1 extends HttpServlet {
	private static final long serialVersionUID = 1L;
	DataAccess model;

	public Servlet1() {
		super();
	}

	@Override
	public void init() {
		model = new DataAccess();

	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		boolean accessResult = model.connect();
		ResultSet rs = null;

		PrintWriter pw = response.getWriter();
		HttpSession session = request.getSession();
		if (accessResult) {
			pw.append("<h1> Ordering </h1><br>");
			session.setAttribute("accessresult", accessResult);
			session.setAttribute("model", model);

			try {
				rs = model.listProducts();
				pw.append("<table style='width:80%'><tr><th>Item</th>" + "<th>Price</th><th>Quantity</th></tr>");
				pw.append("<form method='post' action='Servlet2'>");

				int i = 0;
				// initiate an order
				while (rs.next()) {
					pw.append("<tr><td>" + rs.getString("name") + "</td>");
					pw.append("<td>" + rs.getDouble("price") + "</td>");
					pw.append("<td><input type='text' name='quantity" + i++ + "'</td>");

				}

				pw.append("<br><br><input type='submit' value='continue'>");
				pw.append("</form>");

			} catch (SQLException e) {
				e.printStackTrace();
			}
		} else
			pw.append("Wooops! something went wrong... no connection");
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}

}
```

## Servlet 2
```java
import java.io.IOException;
import java.io.PrintWriter;
import java.sql.ResultSet;
import java.sql.SQLException;
import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/Servlet2")
public class Servlet2 extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public Servlet2() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		ResultSet rs = null;
		ServletConfig grandsum;
		PrintWriter pw = response.getWriter();
		HttpSession session = request.getSession();
		DataAccess model = (DataAccess) session.getAttribute("model");
		if ((boolean) session.getAttribute("accessresult")) {
			pw.append("<h1> Summary </h1><br>");

			try {
				rs = model.listProducts();
				pw.append("<table style='width:80%'><tr><th>Item</th>"
						+ "<th>Price</th><th>Quantity</th><th>Total</th></tr>");
				pw.append("<form method='post' action='Servlet3'>");
				int quantity, index = 0;
				double sum = 0, subTotal;

				while (rs.next()) {
					pw.append("<tr><td>" + rs.getString("name") + "</td>");
					pw.append("<td>" + rs.getDouble("price") + "</td>");
					quantity = Integer.parseInt(request.getParameter("quantity" + index++));
					pw.append("<td>" + quantity + "</td>");
					subTotal = quantity * rs.getDouble("price");
					sum += subTotal;
					pw.append("<td>" + subTotal + "</td>");
				}
				pw.append("</table>");

				// Grand sum of all orders throughout the session
				// if (session.getAttribute("TotalSum") == null)
				if (request.getServletContext().getAttribute("grandsum") == null)
					request.getServletContext().setAttribute("grandsum", "0");

				double taxAmount = Math.round(sum * 0.13 * 100) / 100.0;
				double orderAmount = Math.round((sum + taxAmount) * 100) / 100.0;

				pw.append("<br><br>HST    $" + taxAmount);
				pw.append("<br><b>Total    $" + orderAmount + "</b>");

				pw.append("<br><br><input type='submit' name='nextpage' value='PlaceOrder'>");

				pw.append("</form>");
				double grandSum = orderAmount
						+ Double.parseDouble(request.getServletContext().getAttribute("grandsum").toString());
				request.getServletContext().setAttribute("grandsum", Math.round(grandSum * 100) / 100.0);

			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}

}
```

## Servlet 3
```java
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/Servlet3")
public class Servlet3 extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public Servlet3() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		HttpSession session = request.getSession();
		PrintWriter pw = response.getWriter();

		pw.append("<h1> Thank You! </h1><br>");
		pw.append("<h5> With your help, we have taken in $");
		pw.append("" + request.getServletContext().getAttribute("grandsum"));
		pw.append(" so far today");
		pw.append("<form method='post' action='Servlet1'>");
		pw.append("<br><br><input type='submit' value='Order Some More'>");
		pw.append("</form>");
		session.invalidate();
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}

}
```