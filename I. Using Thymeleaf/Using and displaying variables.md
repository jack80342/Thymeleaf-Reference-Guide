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
如你所见，我们仍旧使用`th:text`属性（这是正确的，因为我们想要替换标签的主体），但是这次语法有点不同。我们使用`${...}`，而不是`#{...}`表达式。这是一个**变量表达式**，使用了`OGNL（对象导航图语言）`。它会在上下文变量的映射关系里被执行。

`${today}`表达式表示“取得叫做today的变量”，然而这些表达式可以变得更为复杂（比如`${user.name}` 指的是取得叫做user的变量，并调用它的for`getName()`方法）。

在属性值的选择上，有相当多的可能性：信息、变量表达式，等等。下一章将展示这些可能性。