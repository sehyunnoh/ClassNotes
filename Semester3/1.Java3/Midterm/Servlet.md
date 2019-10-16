
## term
> deployment descriptor (web.xml)
>   - welcome files, servlet names and descriptions, error pages  

> servlet annotation
>   - @WebServlet("URLPattern")
>   - @WebServlet( { “/AnnotationTest”, “/SayHello” } ) 
>   - @WebServlet(name = "ThisIsTheServletNameNotTheURL", description = "This is our servlet description", urlPatterns= {"/AnnotationTest", "/SayHello"}, asyncSupported= false )

> Welcome files
> ```xml
> <welcome-file-list> 
>    <welcome-file>ExpenseForm.html</welcome-file> 
>    <welcome-file>index.html</welcome-file> 
> </welcome-file-list>
> ```

> Error pages
> ```xml
> <error-page> 
>    <error-code>404</error-code> 
>    <location>/pageNotFound.html</location> 
>    <exception-type>java.lang.NumberFormatException</exception-type> 
>    <location>/error.html</location> 
> </error-page>
> ```

## source
```java
res.setContentType("text/html"); 
PrintWriter out = res.getWriter(); 
out.println("<HTML><HEAD><TITLE>Hello World!</TITLE>"+ 
"</HEAD><BODY>Hello World!</BODY></HTML>"); 
out.close();
```


1. redirect
   - response.sendRedirect("test");
   - request는 못 넘김, 단지 page만 이동
   - request를 수정하면 redirect를 할 수 없다.
   - 이동 후의 request는 전혀 다른 객체이다.
   - 작업이 클라이언트에서 발생
   - url이 변경된다. 

2. dispatch
   - request.getRequestDispatcher("testDispatch2").forward(request, response);
   - getServletContext().getRequestDispatcher("testDispatch2").forward(request, response);
   - request 자체를 넘기는 방식
   - 작업이 서버에서 발생
   - url 변경 안됨 (최소 호출한 url이 그대로 있음) 

## POJO & JavaBeans

## GET vs post
![GP](images/get_post.jpg)

## getParameter vs getAttribute
![gpa](images/parameter_attribute.jpeg)
