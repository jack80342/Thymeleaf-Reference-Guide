### 使用和显示变量

现在，让我们给主页添加更多内容。比如，我们可能想要在欢迎信息下面显示日期，就像这样：
```
Welcome to our fantastic grocery store!

Today is: 12 july 2010
```
首先，我们要修改controller，把日期作为上下文变量添加进去：
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