## date.jsp
```jsp
<p>Today's date: 
    <% out.print(new java.util.Date()); %>
</p>
```

## actionTag.jsp
```jsp
    <h2>The include action Example</h2>
    <jsp:include page="date.jsp" />
```