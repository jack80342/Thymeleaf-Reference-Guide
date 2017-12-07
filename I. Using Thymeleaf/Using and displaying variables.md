### 使用和显示变量

Now let’s add some more content to our home page. For example, we may want to display the date below our welcome message, like this:
```
Welcome to our fantastic grocery store!

Today is: 12 july 2010
```
First of all, we will have to modify our controller so that we add that date as a context variable:
```java
public void process(
            final HttpServletRequest request, final HttpServletResponse response,
            final ServletContext servletContext, final ITemplateEngine templateEngine)
            throws Exception {
        
    SimpleDateFormat dateFormat = new SimpleDateFormat("dd MMMM yyyy");
    Calendar cal = Calendar.getInstance();
        
    WebContext ctx = 
            new WebContext(request, response, servletContext, request.getLocale());
    ctx.setVariable("today", dateFormat.format(cal.getTime()));
        
    templateEngine.process("home", ctx, response.getWriter());
        
}
```
We have added a `String` variable called `today` to our context, and now we can display it in our template:
```html
<body>

  <p th:utext="#{home.welcome}">Welcome to our grocery store!</p>

  <p>Today is: <span th:text="${today}">13 February 2011</span></p>
  
</body>
```
As you can see, we are still using the `th:text` attribute for the job (and that’s correct, because we want to replace the tag’s body), but the syntax is a little bit different this time and instead of a `#{...}` expression value, we are using a `${...}` one. This is a **variable expression**, and it contains an expression in a language called `OGNL (Object-Graph Navigation Language)` that will be executed on the context variables map we talked about before.

The `${today}` expression simply means “get the variable called today”, but these expressions could be more complex (like `${user.name}` for “get the variable called user, and call its `getName()` method”).

There are quite a lot of possibilities in attribute values: messages, variable expressions… and quite a lot more. The next chapter will show us what all these possibilities are.