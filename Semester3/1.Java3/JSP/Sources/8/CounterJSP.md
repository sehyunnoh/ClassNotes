![CounterJSP](../images/CounterJSP.jpg)

## Counter.java
```java
package counterJsp;

public class Counter {
	private static int count=0;
	public static synchronized int getCount() {
		count ++;
		return count;
	}

}
```

## Newfile.jsp
```jsp
<%@ page import="counterJsp.Counter"%> 
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>

<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
<%!Counter c = new Counter(); %>
<h1>Number of visits so far <%= c.getCount()%></h1>

</body>
</html>
```