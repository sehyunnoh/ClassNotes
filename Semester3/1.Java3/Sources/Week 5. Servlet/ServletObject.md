## NewStudent.html
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>New Student</title>
</head>
<body>
	<form method="post" action="ProcessData">
		First Name: <input type="text" name="first"> Student Id: <input
			type="number" name="id"> <br>Java Version:<br> Java
		SE<input type="radio" name="API" value="Java SE"> Java EE<input
			type="radio" name="API" value="Java EE"> Java ME<input
			type="radio" name="API" value="Java ME"> <input type="submit"
			value="Create">
	</form>

</body>
</html>
```

## ProcessData.data
```java

import java.io.IOException;
import java.io.PrintWriter;
import java.util.List;
import java.util.concurrent.CopyOnWriteArrayList;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/ProcessData")
public class ProcessData extends HttpServlet {
	private static final long serialVersionUID = 1L;
	List<Student> studentList = new CopyOnWriteArrayList<Student>();

	public ProcessData() {
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.getWriter().append("Served at: ").append(request.getContextPath());
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		String firstname = request.getParameter("first");
		int sID = Integer.parseInt(request.getParameter("id"));
		String[] api = request.getParameterValues("API");
		PrintWriter pw = response.getWriter();
		response.setContentType("text/html");
		// pw.append("<br> <h2>" + firstname + " " + sID + " " + api[0]);

		Student student = new Student(firstname, sID, api[0]);
		studentList.add(student);
		for (Student st : studentList)
			pw.append("<h2> " + st);
	}

}
```

## Student.java
```java

public class Student {

	private String firstName;
	private int sID;
	private String javaVersion;

	public Student() {
	}

	public Student(String firstName, int sID, String javaVersion) {
		super();
		this.firstName = firstName;
		this.sID = sID;
		this.javaVersion = javaVersion;
	}

	public String getFirstName() {
		return firstName;
	}

	public void setFirstName(String firstName) {
		this.firstName = firstName;
	}

	public int getsID() {
		return sID;
	}

	public void setsID(int sID) {
		this.sID = sID;
	}

	public String getJavaVersion() {
		return javaVersion;
	}

	public void setJavaVersion(String javaVersion) {
		this.javaVersion = javaVersion;
	}

	@Override
	public String toString() {
		return String.format("%20s %10d %15s", firstName, sID, javaVersion);
	}

}
```