## main.html
```html
<body>
	<form method="post" action="index.jsp">
		Circle Radius <input type="text" name="radiusSize"> <input
			type="submit" value="Go">
	</form>
</body>
```

## index.jsp
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

	<%!public double computeArea(double radius) {
  			return Math.PI*radius*radius;
	}%>
	<div>
		<%
		double r=0;
 		try{
			 r= Double.parseDouble(request.getParameter("radiusSize"));
			 out.print("The area of a circle with radius of " + r + " = " + computeArea(r));
		 }
		catch (NumberFormatException e){
      		System.out.println("Something went wrong");
      		out.print("It is not a double!");
      	}
	    %>
	</div>
</body>
</html>
```