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
		<label>Make: </label><input type="text" name="make">
		<label>Year: </label><input type="text" name="year">
		<label>Color: </label><input type="text" name="color">
		<input type="submit" name="button" value="new">
		<input type="submit" name="button" value="done">
	</form>
</body>
</html>
```

## Controller.java
```java

import java.io.IOException;
import java.util.ArrayList;

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
	}
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		String button = request.getParameter("button");
		if (button.equals("new")) {
			// new car object
			Car c = new Car();
			c.setMake(request.getParameter("make"));
			c.setColor(request.getParameter("color"));
			c.setYear(Integer.parseInt(request.getParameter("year")));
			carList.add(c);
			response.sendRedirect("New.jsp");
		} else { // no more car objects
			request.setAttribute("cars", carList);
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

## view.jsp
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
	<table style="width: 80%">
		<tr style="color: white; background-color: green">
			<td>${cars[0].make}</td>
			<td>${cars[0].color}</td>
			<td>${cars[0].year}</td>
		</tr>
		<tr style="color: white; background-color: yellow">
			<td>${cars[1].make}</td>
			<td>${cars[1].color}</td>
			<td>${cars[1].year}</td>
		</tr>
		<tr style="color: white; background-color: green">
			<td>${cars[2].make}</td>
			<td>${cars[2].color}</td>
			<td>${cars[2].year}</td>
		</tr>
	</table>
</body>
</html>
```