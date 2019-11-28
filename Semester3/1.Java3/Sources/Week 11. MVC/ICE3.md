[ICE3](../images/ICE3.jpg)

## index.jsp
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
	<hr />
	<h1>Tip Calculator</h1>
	<hr />
	<form action='Controller' method='post'>
		Bill Amount: $ <input type='text' name='amt' /> <br /> Select a
		Tip%: <select name='tip'>
			<option value='1'>None</option>
			<option value='5'>5%</option>
			<option value='10'>10%</option>
			<option value='15'>15%</option>
			<option value='20'>20%</option>
			<option value='25'>25%</option>
		</select> <br /> <input type='submit' value='calculate' />
	</form>
</body>
</html>
```

## Controller.java
```java
package Controller;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import javafx.scene.shape.Circle;
import model.Bill;

@WebServlet("/Controller")
public class Controller extends HttpServlet {
	private static final long serialVersionUID = 1L;

	Bill b;

	public Controller() {
		b = new Bill();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		b.setAmt(Double.parseDouble(request.getParameter("amt")));
		b.setTip(Integer.parseInt(request.getParameter("tip")));

		double result = b.calcTip(b.getAmt(), b.getTip());

		request.setAttribute("amt", b.getAmt());
		request.setAttribute("tip", b.getTip());
		request.setAttribute("result", result);
		RequestDispatcher rd = request.getRequestDispatcher("view.jsp");
		rd.forward(request, response);

	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}

}
```

## Bill.java
```java
package model;

public class Bill {
	private double amt;
	private int tip;

	public Bill() {
		super();
	}

	public Bill(double amt, int tip) {
		super();
		this.amt = amt;
		this.tip = tip;
	}

	public double getAmt() {
		return amt;
	}

	public void setAmt(double amt) {
		this.amt = amt;
	}

	public int getTip() {
		return tip;
	}

	public void setTip(int tip) {
		this.tip = tip;
	}

	public double calcTip(double amt, int tip) {
		return amt * tip / 100;
	}

}
```

## view.jsp
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
	<div>
		<hr />
		<h1>Tip Calculator</h1>
		<hr />
		<br>
		<br> Tip$ for $ ${amt} bill @ ${tip} %: $ ${result}
	</div>
</body>
</html>
```