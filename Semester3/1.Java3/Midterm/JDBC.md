```java
// option 임 (예전 버전이면 필수로 넣어줘야 되는데, 지금은 안 넣어줘도 됨.)))
public DataAccess() {
	try {
        Class.forName("com.mysql.jdbc.Driver");
    } catch (ClassNotFoundException e) {
    	// library 포함 안 되어 있으면 이 error 남.
        System.err.println("ERROR: mysql.com.jdbc.Driver not found.");
        System.exit(0);
    }
}
```
 - Note: if you are using a different database or an older version of JDBC, you  may still be required to load the driver manually (but in practice it almost never happens)


## JDBC
- DriverManager : used to load or select JDBC drivers 
- Driver : used to connect to the native database 
- Connection : creates a session with the database 
- Statement : represents an individual SQL statement 
- PreparedStatement : the state of the art in SQL data management 
- ResultSet : a collection of rows returned from the database as the result from a single query

1. Load the JDBC Driver 
2. Establish a connection to the database 
3. Create a PreparedStatement object (from the connection!) 
4. Execute some SQL statement(s) 
5. Process the ResultSet (if the SQL Statement is a query) 
6. Close the JDBC object