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
我们已经往上下文里添加了`String`变量`today`。现在我们就可以在模版里显示它了：
```html
<body>

  <p th:utext="#{home.welcome}">Welcome to our grocery store!</p>

  <p>Today is: <span th:text="${today}">13 February 2011</span></p>
  
</body>
```
如你所见，我们仍旧使用`th:text`属性（这是正确的，因为我们想要替换标签的主体），但是这次语法有点不同，我们使用`${...}`，而不是`#{...}`表达式。This is a **variable expression**, and it contains an expression in a language called `OGNL (Object-Graph Navigation Language)` that will be executed on the context variables map we talked about before.

The `${today}` expression simply means “get the variable called today”, but these expressions could be more complex (like `${user.name}` for “get the variable called user, and call its `getName()` method”).

There are quite a lot of possibilities in attribute values: messages, variable expressions… and quite a lot more. The next chapter will show us what all these possibilities are.