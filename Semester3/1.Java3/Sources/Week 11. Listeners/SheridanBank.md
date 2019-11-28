[sheridanbank](../images/SheridanBank.jpg)

## index.jsp
```jsp


<%@page contentType="text/html" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>Sheridan Bank</title>
    </head>
    <body>
        <div id="adminLink" style="text-align:right">
            <a href='<%= response.encodeURL("admin/admin_main.jsp")%>'>
                Administrator Main Page
            </a>
        </div>
        <h1 style='text-align:center'>Welcome to Sheridan Bank!</h1>
        <form action='<%= response.encodeURL("GoToUserMain.do") %>' method="POST">
            <table style="margin-left:auto;margin-right:auto">
                <tr>
                    <td>Enter Username:</td>
                    <td><input type="text" name="username" /></td>
                </tr>
                <tr>
                    <td colspan="2" style="text-align:center">
                        <input type="submit" value="User Main Page"/>
                    </td>
                </tr>
            </table>
        </form>
    </body>
</html>
```

## GoToUserMainServlet.java
```java
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */

package com.sheridanbank.servlets;

import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import com.sheridanbank.business.User;
import com.sheridanbank.dao.UserDAO;
import com.sheridanbank.db.DBConnection;

@WebServlet("/GoToUserMain.do")
public class GoToUserMainServlet extends HttpServlet {

	@Override
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

	}

	@Override
	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		// TODO: Get the username from the request
		String username = request.getParameter("username");
		
		// TODO: Get the DBConnection object stored in the ServletContext for
		// use by the DAO classes
		ServletContext sc = getServletConfig().getServletContext();
		String driver = "com.mysql.jdbc.Driver";
		String url = "" + sc.getAttribute("url");
		String database = "sheridanbank";
		String user = "" + sc.getAttribute("user");
		String pw = "" + sc.getAttribute("pw");

		DBConnection db = new DBConnection(driver, url, database, user, pw);
		
		// TODO: Get the user information based on the username
		UserDAO userDAO = new UserDAO();
		User userInfo = userDAO.getUser(db.getConnection(), username);
		
		// TODO: Store the User object returned in the session (?)

		// TODO: Forward the request to user_main.jsp
		request.setAttribute("user", userInfo);
		request.getRequestDispatcher("user_main.jsp").forward(request, response);
	}

	/**
	 * Returns a short description of the servlet.
	 * 
	 * @return a String containing servlet description
	 */
	@Override
	public String getServletInfo() {
		return "Short description";
	}// </editor-fold>

}

```

## user_main.jsp
```jsp


<%@page contentType="text/html" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>Sheridan Bank</title>
    </head>
    <body>
        <jsp:useBean id="user" scope="session" class="com.sheridanbank.business.User" />
        <h1 style="text-align:center">
            Welcome, <jsp:getProperty name="user" property="firstName" />
            <jsp:getProperty name="user" property="lastName" />
        </h1>
    </body>
</html>
```

## admin_main.jsp
```jsp


<%@page contentType="text/html" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>Sheridan Bank</title>
    </head>
    <body>
        <h1 style="text-align:center">Administrator Main Page</h1>
        <a href='<%= response.encodeURL("addUser.jsp") %>'>Add New User</a>
    </body>
</html>
```

## addUser.jsp
```jsp


<%@page contentType="text/html" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>Sheridan Bank</title>
    </head>
    <body>
        <h1 style="text-align:center">Add New User</h1>
        <form action='<%= response.encodeURL("AddUser.do") %>' method="POST">
            <table style="margin-left:auto;margin-right:auto">
                <tr>
                    <td style="text-align:right">Username:</td>
                    <td><input type="text" name="username" /></td>
                </tr>
                <tr>
                    <td style="text-align:right">Password:</td>
                    <td><input type="text" name="password" /></td>
                </tr>
                <tr>
                    <td style="text-align:right">Role:</td>
                        <td>
                            <select name="role">
                                <option>admin</option>
                                <option>manager</option>
                                <option selected>user</option>
                            </select>
                        </td>
                </tr>
                <tr>
                    <td style="text-align:right">First Name:</td>
                    <td><input type="text" name="first" /></td>
                </tr>
                <tr>
                    <td style="text-align:right">Last Name:</td>
                    <td><input type="text" name="last" /></td>
                </tr>
                <tr>
                    <td colspan="2" style="text-align:center">
                       <input type="submit" value="Add User"/> 
                    </td>
                </tr>
            </table>
        </form>
    </body>
</html>

```

## web.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="http://xmlns.jcp.org/xml/ns/javaee"
	xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
	id="WebApp_ID" version="4.0">
	<display-name>SheridanBank</display-name>
	<welcome-file-list>
		<welcome-file>index.html</welcome-file>
		<welcome-file>index.htm</welcome-file>
		<welcome-file>index.jsp</welcome-file>
		<welcome-file>default.html</welcome-file>
		<welcome-file>default.htm</welcome-file>
		<welcome-file>default.jsp</welcome-file>
	</welcome-file-list>

	<listener>
		<listener-class>com.sheridanbank.listeners.DBConnectionListener</listener-class>
	</listener>
</web-app>
```

## AddUserServlet.java
```java
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */

package com.sheridanbank.servlets;

import java.io.IOException;
import java.io.PrintWriter;
import java.sql.Connection;
import javax.servlet.RequestDispatcher;
import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import com.sheridanbank.business.User;
import com.sheridanbank.dao.UserDAO;
import com.sheridanbank.db.DBConnection;

@WebServlet("/admin/AddUser.do")
public class AddUserServlet extends HttpServlet {
       
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
        
    } 

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
        
        // TODO: Get the new user information based on the request parameters
    	String username = request.getParameter("username");
    	String password = request.getParameter("password");
    	String role = request.getParameter("role");
    	String first = request.getParameter("first");
    	String last = request.getParameter("last");       
        
        // TODO: Get the DBConnection object from the ServletContext
    	ServletContext sc = getServletConfig().getServletContext();
		String driver = "com.mysql.jdbc.Driver";
		String url = "" + sc.getAttribute("url");
		String database = "sheridanbank";
		String user = "" + sc.getAttribute("user");
		String pw = "" + sc.getAttribute("pw");

		DBConnection db = new DBConnection(driver, url, database, user, pw);
        
        // TODO: Add the User to the database
		UserDAO userDAO = new UserDAO();
		User userInfo = new User(username, password, role, first, last);
		
		boolean result = userDAO.addUser(db.getConnection(), userInfo);		
        
        // TODO: Forward the request to the admin main page
		request.getRequestDispatcher("admin_main.jsp").forward(request, response);
        
    }

    @Override
    public String getServletInfo() {
        return "Short description";
    }// </editor-fold>

}

```

## User.java
```java
/*
 * A User JavaBean
 */

package com.sheridanbank.business;

import java.io.Serializable;


public class User {
    private int userId;
    private String username;
    private String password;
    private String role;
    private String firstName;
    private String lastName;
    
    public User() {
        userId = 0;
        username = "";
        password = "";
        role = "";
        firstName = "";
        lastName = "";
    }
    
    public User(String username, String password, String role, String firstName,
            String lastName) {
        this(0, username, password, role, firstName, lastName);
    }
    
    public User(int userId, String username, String password, String role,
            String firstName, String lastName) {
        this.userId = userId;
        this.username = username;
        this.password = password;
        this.role = role;
        this.firstName = firstName;
        this.lastName = lastName;
    }

    /**
     * @return the userId
     */
    public int getUserId() {
        return userId;
    }

    /**
     * @param userId the userId to set
     */
    public void setUserId(int userId) {
        this.userId = userId;
    }

    /**
     * @return the username
     */
    public String getUsername() {
        return username;
    }

    /**
     * @param username the username to set
     */
    public void setUsername(String username) {
        this.username = username;
    }

    /**
     * @return the password
     */
    public String getPassword() {
        return password;
    }

    /**
     * @param password the password to set
     */
    public void setPassword(String password) {
        this.password = password;
    }

    /**
     * @return the role
     */
    public String getRole() {
        return role;
    }

    /**
     * @param role the role to set
     */
    public void setRole(String role) {
        this.role = role;
    }

    /**
     * @return the firstName
     */
    public String getFirstName() {
        return firstName;
    }

    /**
     * @param firstName the firstName to set
     */
    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    /**
     * @return the lastName
     */
    public String getLastName() {
        return lastName;
    }

    /**
     * @param lastName the lastName to set
     */
    public void setLastName(String lastName) {
        this.lastName = lastName;
    }
    
}
```

## UserDAO.java
```java
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */

package com.sheridanbank.dao;

import java.sql.*;
import com.sheridanbank.business.User;
import com.sheridanbank.db.DBConnection;


public class UserDAO {

    @SuppressWarnings("finally")
	public User getUser(Connection conn, String username) {
        User user = null;

        PreparedStatement ps = null;
        ResultSet rs = null;

        try {
            String sql = "SELECT * FROM User WHERE Username = ?";

            ps = conn.prepareStatement(sql);
            ps.setString(1, username);

            rs = ps.executeQuery();

            while (rs.next()) {
                // Get the user info
                int userId = rs.getInt("UserId");
                String password = rs.getString("Password");
                String role = rs.getString("Role");
                String firstName = rs.getString("FirstName");
                String lastName = rs.getString("LastName");
                
                // Initialize the user return variable
                user = new User(userId, username, password, role, firstName, lastName);
            }

        } catch (SQLException e) {
            System.err.println("SQLException: " + e.getMessage());
        } finally {
            DBConnection.closeJDBCObjects(conn, ps, rs);
            return user;
        }
    }
    
    @SuppressWarnings("finally")
	public boolean addUser(Connection conn, User user) {
        boolean success = false;
        
        // Declare JDBC objects
        PreparedStatement ps = null;
        
        try {
            String sql = "INSERT INTO User(Username, Password, Role, " +
                        " FirstName, LastName) VALUES(?, ?, ?, ?, ?);";
            
            ps = conn.prepareStatement(sql);
            ps.setString(1, user.getUsername());
            ps.setString(2, user.getPassword());
            ps.setString(3, user.getRole());
            ps.setString(4, user.getFirstName());
            ps.setString(5, user.getLastName());
            
            int count = ps.executeUpdate();
            
            if (count > 0) {
                success = true;
            }
            
        } catch (SQLException e) {
            System.err.println("SQLException: " + e.getMessage());
        } finally {
            DBConnection.closeJDBCObjects(conn, ps);
            return success;
        }
    }
}

```

## DBConnection.java
```java
/*
 * A class used to establish JDBC Connections.
 */

package com.sheridanbank.db;

import java.sql.*;


public class DBConnection {
    private String url;
    private String username;
    private String password;
    
    /*
     * Loads the driver class and set the required properties when establishing
     * a Connection.
     */
    public DBConnection(String driver, String url, String database,
            String username, String password) {
        
        try {
            Class.forName(driver);
        } catch(ClassNotFoundException e) {
            System.out.println("ERROR: Exception loading driver class");
        }

        this.url = url + database;
        this.username = username;
        this.password = password;
    }

    /*
     * Method that outside classes will use to get a Connection object.
     * Note that if this method causes an SQLException, it is thrown to the
     * class that called getConnection().
     */    
    public Connection getConnection() {
        Connection conn = null;
        try {
            conn = DriverManager.getConnection(url, username, password);
        } catch (SQLException e) {
            System.err.println("Exception creating Connection object");
        } finally {
            return conn;
        }
        
    }
    
    public static void closeJDBCObjects(Connection conn, Statement stmt, ResultSet rs) {
        try {
            if (rs != null) {
                rs.close();
            }
            
            if (stmt != null) {
                stmt.close();
            }
            
            if (conn != null) {
                conn.close();
            }
        } catch (SQLException ignored) {
        }
    }
    
    public static void closeJDBCObjects(Connection conn, Statement stmt) {
        closeJDBCObjects(conn, stmt, null);
    }
}

```

## DBConnectionListener.java
```java
package com.sheridanbank.listeners;

import javax.servlet.ServletContext;
import javax.servlet.ServletContextAttributeListener;
import javax.servlet.ServletContextEvent;
import javax.servlet.ServletContextListener;
import javax.servlet.annotation.WebListener;

@WebListener
public class DBConnectionListener implements ServletContextListener, ServletContextAttributeListener {

	public DBConnectionListener() {
	}

	public void contextInitialized(ServletContextEvent sce) {
		ServletContext sc = sce.getServletContext();
		sc.setAttribute("user", "root");
		sc.setAttribute("pw", "");
		sc.setAttribute("url", "jdbc:mysql://localhost:3306/");
	}
	
	public void contextDestroyed(ServletContextEvent event) {
	}

}

```