```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  <display-name>Exercise4</display-name>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
  </welcome-file-list>
</web-app>
```

## mapping
```xml
  <servlet>
  	<servlet-name>servletTest</servlet-name>
  	<servlet-class>Test</servlet-class>
  </servlet>
  <servlet-mapping>
  	<servlet-name>servletTest</servlet-name>
  	<url-pattern>/test</url-pattern>
  </servlet-mapping>
```
## Welcome files
```xml
<welcome-file-list> 
   <welcome-file>ExpenseForm.html</welcome-file> 
   <welcome-file>index.html</welcome-file> 
</welcome-file-list>
```

## Error pages
```xml
<error-page> 
   <error-code>404</error-code> 
   <location>/pageNotFound.html</location> 
   <exception-type>java.lang.NumberFormatException</exception-type> 
   <location>/error.html</location> 
</error-page>
```
