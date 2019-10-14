## SumServlet.java
```java
package ca.sheridancollege.controllers;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/Sum")
public class SumServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public SumServlet() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		String cal = request.getParameter("cal");
		String number1 = request.getParameter("first");
		String number2 = request.getParameter("second");

		double d1 = Double.valueOf(number1);
		double d2 = Double.valueOf(number2);

		response.setContentType("text/html");
		PrintWriter pr = response.getWriter();

		try {

			double result = 0;
			String resultText = "";
			String symbol = "";
			switch (cal) {
			case "p": // plus
				resultText = "Plus";
				symbol = "+";
				result = d1 + d2;
				break;
			case "m": // minus
				resultText = "Minus";
				symbol = "-";
				result = d1 - d2;
				break;
			case "mm": // multiply
				resultText = "Mutiply";
				symbol = "*";
				result = d1 * d2;
				break;
			case "d": // division
				resultText = "Division";
				symbol = "/";
				result = d1 / d2;
				break;
			default:
				break;
			}

			if (cal.equals("d") && d2 == 0) {
				pr.append("<p>divide 0 is not allowed<p>");
			} else {
				pr.append(resultText);
				pr.append("<P><h2>" + d1 + " " + symbol + " " + d2 + " = " + result);
			}

		} catch (Exception e) {
			pr.append("divide 0 is allowed ");
		}

	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}

}
```

## AddtwoNumbers.html
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<form method="post" action="Sum">
		<input type="radio" name="cal" value="p" checked> Plus <input
			type="radio" name="cal" value="m"> Minus <input type="radio"
			name="cal" value="mm"> Multiply <input type="radio"
			name="cal" value="d"> Division<br>
		<br> <label>num1: </label> <input type="text" name="first"><br>
		<label>num2: </label> <input type="text" name="second"> <input
			type="submit" value="Cal">

	</form>
</body>
</html>
```