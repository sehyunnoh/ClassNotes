## new.jsp
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
	<form method="post" action="Controller">
		<label>Make: </label><input type="text" name="make"> <label>Year:
		</label><input type="text" name="year"> <label>Color: </label><select
			name="colors">
			<option>Black</option>
			<option>Blue</option>
			<option>Red</option>
			<option>Silver</option>
			<option>While</option>
		</select> <input type="submit" name="button" value="new"> <input
			type="submit" name="button" value="done">
	</form>
</body>
</html>
```

## Controller.java
```java

import java.io.IOException;
import java.util.Date;
import java.util.ArrayList;
import java.util.Calendar;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import model.Car;

@WebServlet("/Controller")
public class Controller extends HttpServlet {
	private static final long serialVersionUID = 1L;
	ArrayList<Car> carList;

	@Override
	public void init() {
		carList = new ArrayList<Car>();
	}

	public Controller() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		String button = request.getParameter("button");
		if (button.equals("new")) {
			Car c = new Car();
			c.setMake(request.getParameter("make"));
			c.setColor(request.getParameterValues("colors")[0]);
			c.setYear(Integer.parseInt(request.getParameter("year")));
			carList.add(c);
			response.sendRedirect("New.jsp");

		} else { // no more car objects
			request.setAttribute("cars", carList);
			Calendar c = Calendar.getInstance();
			c.setTime(new Date());
			request.setAttribute("thisYear", c.get(Calendar.YEAR));
			request.getRequestDispatcher("View.jsp").forward(request, response);
		}
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}

}
```

## Car.java
```java
package model;

import java.io.Serializable;

public class Car implements Serializable {

	private static final long serialVersionUID = 1L;
	private String make;
	private String color;
	private int year;

	public String getMake() {
		return make;
	}

	public void setMake(String make) {
		this.make = make;
	}

	public String getColor() {
		return color;
	}

	public void setColor(String color) {
		this.color = color;
	}

	public int getYear() {
		return year;
	}

	public void setYear(int year) {
		this.year = year;
	}

	public Car() {
	}
}
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
<title>Insert title here</title>
<style>
tr:nth-child(even) {
	background-color: blue
}

tr:nth-child(odd) {
	background-color: green
}
</style>
</head>
<body>
	<table style="width: 80%">
		<tr style="color: black; background-color: yellow">
			<th>Make</th>
			<th>Color</th>
			<th>Year</th>
			<th>isEmission?</th>
		</tr>

		<c:forEach var="car" items="${cars}">
			<tr style="color: white">
				<td>${car.make}</td>
				<td>${car.color}</td>
				<td>${car.year}</td>
				<c:if test="${thisYear >= 7}">
					<td style="color: red">Yes</td>
				</c:if>
			</tr>
		</c:forEach>

	</table>

</body>
</html>
```