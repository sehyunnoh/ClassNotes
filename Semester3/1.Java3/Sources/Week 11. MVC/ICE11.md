[ICE11](../images/ICE11.jpg)

## form.jsp
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>ICE 11_1</title>
</head>
<body>
	<sql:setDataSource var="db" driver="com.mysql.jdbc.Driver"
		url="jdbc:mysql://localhost:3306/SheridanUsedCars" user="root"
		password="" />

	<sql:query dataSource="${db}" var="result">SELECT * FROM 
manufacturer</sql:query>

	<form method="post" action="Controller">
		<select name="manufacturer">
			<c:forEach items="${result.rows}" var="row">
				<option value="${row.manufacturerID}">${row.manufacturer}</option>
			</c:forEach>
		</select> <br> <input type="text" placeholder="max price" name="maxPrice"> <input type="submit">
	</form>

</body>
</html>
```

## Controller.java
```java
package ca.sheridancollege.controller;

import java.io.IOException;
import java.util.ArrayList;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import ca.sheridancollege.beans.Car;
import ca.sheridancollege.dao.DAO;

@WebServlet("/Controller")
public class Controller extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public Controller() {
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		int manuId = Integer.parseInt(request.getParameter("manufacturer"));
		double maxPrice = Double.parseDouble(request.getParameter("maxPrice"));

		DAO dao = new DAO();
		ArrayList<Car> list = dao.select(manuId, maxPrice);

		request.setAttribute("carlist", list);
		request.getRequestDispatcher("view.jsp").forward(request, response);

	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}

}
```

## Car.java
```java
package ca.sheridancollege.beans;

public class Car {

	private String manufacturer;
	private String model;
	private int year;
	private String colour;
	private double price;

	public Car(String manufacturer, String model, int year, String colour, double price) {
		this.manufacturer = manufacturer;
		this.model = model;
		this.year = year;
		this.colour = colour;
		this.price = price;
	}

	public String getManufacturer() {
		return manufacturer;
	}

	public void setManufacturer(String manufacturer) {
		this.manufacturer = manufacturer;
	}

	public String getModel() {
		return model;
	}

	public void setModel(String model) {
		this.model = model;
	}

	public int getYear() {
		return year;
	}

	public void setYear(int year) {
		this.year = year;
	}

	public String getColour() {
		return colour;
	}

	public void setColour(String colour) {
		this.colour = colour;
	}

	public double getPrice() {
		return price;
	}

	public void setPrice(double price) {
		this.price = price;
	}

}
```

## DAO.java
```java
package ca.sheridancollege.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.ArrayList;

import ca.sheridancollege.beans.Car;

public class DAO {

	String url = "jdbc:mysql://localhost:3306/SheridanUsedCars";
	String id = "root";
	String pw = "";

	public DAO() {
		try {
			Class.forName("com.mysql.jdbc.Driver");
		} catch (ClassNotFoundException e) {
			System.out.println("ERROR: Exception loading driver class");
		}
		
	}

	public ArrayList<Car> select(int manuId, double maxPrice) {
		ArrayList<Car> list = new ArrayList<Car>();

		Connection con = null;
		PreparedStatement pstmt = null;
		ResultSet res = null;

		try {
			con = DriverManager.getConnection(url, id, pw);
			String sql = "   SELECT m.manufacturer, c.model, c.year, c.colour, c.price\r\n"
					+ "  FROM car c, manufacturer m\r\n" + " WHERE c.manufacturerID = m.manufacturerID\r\n"
					+ "   AND m.manufacturerID = ?" + "   AND c.price <= ?";
			pstmt = con.prepareStatement(sql);
			pstmt.setInt(1, manuId);
			pstmt.setDouble(2, maxPrice);
			res = pstmt.executeQuery();
			while (res.next()) {
				String manufacturer = res.getString(1);
				String model = res.getString(2);
				int year = res.getInt(3);
				String colour = res.getString(4);
				double price = res.getDouble(5);

				Car car = new Car(manufacturer, model, year, colour, price);
				list.add(car);
			}
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			try {
				if (res != null)
					res.close();
				if (pstmt != null)
					pstmt.close();
				if (con != null)
					con.close();
			} catch (Exception e2) {
				e2.printStackTrace();
			}
		}

		return list;
	}

}
```

## view.jsp
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Car List</title>
<style>
th {
	background: yellow
}

tr:nth-child(even) {
	background: #CCC
}

td, th {
	border: 1px solid black;
	text-align: center;
}
</style>
</head>
<body>
	<table>
		<tr>
			<th>manufacturer</th>
			<th>model</th>
			<th>year</th>
			<th>colour</th>
			<th>price</th>
		</tr>
		<c:forEach items="${carlist}" var="val">
			<tr>
				<td>${val.manufacturer}</td>
				<td>${val.model}</td>
				<td>${val.year}</td>
				<td>${val.colour}</td>
				<td>${val.price}</td>
			</tr>
		</c:forEach>
	</table>
</body>
</html>
```