```java
@WebServlet("/OrderServlet")
public class OrderServlet extends HttpServlet {

	private double totalSum;

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		out.append("		<div class='price' id='price'>");
		out.append(             makePrice(size, numbers));
		out.append("		</div>");
		out.append("		<br>");
		out.append("		<div id='totalSum'>So far, we have made $" + String.format("%.2f", totalSum) + "</div>");
		out.append("	</div>");
	}

	// make price and store totam sum
	public String makePrice(String size, int numbers) {
		double price = 0;
		if (size.equals("small")) {
			price = 1.2;
		} else if (size.equals("medium")) {
			price = 1.5;
		} else if (size.equals("large")) {
			price = 1.8;
		} else if (size.equals("exLarge")) {
			price = 2.0;
		} else {
			price = 1.2;
		}

		totalSum += (price * 1.13 * numbers);
		return String.format("Cost: $%.2f x %d + tax = $%.2f", price, numbers, (price * 1.13 * numbers));
	}
	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		doGet(request, response);
	}

}
```