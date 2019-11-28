## SumServlet.java

```java
package sheridan.sehyun.week5;
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

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String number1 = request.getParameter("first");
		String number2 = request.getParameter("second");
		int result = Integer.parseInt(number1) + 
				     Integer.parseInt(number2);
		PrintWriter pr = response.getWriter();
		pr.append("<P><h2>" + number1 + " + " + number2 + " = " + result);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doGet(request, response);
	}

}
```