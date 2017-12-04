### 上下文

为了处理我们的模版，我们将会创建一个实现了`IGTVGController`接口的`HomeController`类。如下：
```java
public class HomeController implements IGTVGController {

    public void process(
            final HttpServletRequest request, final HttpServletResponse response,
            final ServletContext servletContext, final ITemplateEngine templateEngine)
            throws Exception {
        
        WebContext ctx = 
                new WebContext(request, response, servletContext, request.getLocale());
        
        templateEngine.process("home", ctx, response.getWriter());
        
    }

}
```
我们第一眼看到的就是上下文的创建。一段Thymeleaf的上下文就是一个实现了`org.thymeleaf.context.IContext`接口的对象。上下文应当包含，在变量的映射关系中执行模版引擎需要的所有数据，同时指明了外部化的信息必须用到的地区。
```java
public interface IContext {

    public Locale getLocale();
    public boolean containsVariable(final String name);
    public Set<String> getVariableNames();
    public Object getVariable(final String name);
    
}
```
这个接口有一个专门的扩展：`org.thymeleaf.context.IWebContext`，用在基于ServletAPI的网络应用里（比如SpringMVC）。
```java
public interface IWebContext extends IContext {
    
    public HttpServletRequest getRequest();
    public HttpServletResponse getResponse();
    public HttpSession getSession();
    public ServletContext getServletContext();
    
}
```
Thymeleaf核心库提供了这些接口里每一个的实现：

- `org.thymeleaf.context.Context`实现了`IContext`接口
- `org.thymeleaf.context.WebContext`实现了`IWebContext`接口

如同你在controller的代码里看到的那样，我们使用了`WebContext`。实际上，我们不得不这样做，因为`ServletContextTemplateResolver`需要一个实现了`IWebContext`接口的上下文。
```java
WebContext ctx = new WebContext(request, response, servletContext, request.getLocale());
```
那四个构造器参数中只有三个是必须的，因为如果没有指定地区（尽管你不应当让这种情况发生在实际的应用里），系统里默认的地区将会被使用。

我们可以使用一些专门的表达式，从模版里的`WebContext`获取请求参数、请求、会话和应用属性。比如：

- `${x}`会返回存储在Thymeleaf上下文里的变量`x`，或者作为请求属性存储的变量`x`。
- `${param.x}`会返回一个称为`x`的请求属性（可能多值）。
- `${session.x}`会返回一个称为`x`的会话属性。
- `${application.x}`会返回一个称为`x`的servlet上下文属性。