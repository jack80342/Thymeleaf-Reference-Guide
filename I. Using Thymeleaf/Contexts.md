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
我们第一眼看到的就是上下文的创建。一段Thymeleaf的上下文就是一个实现了`org.thymeleaf.context.IContext`接口的对象。上下文应当包含在变量的映射关系中执行模版引擎需要的所有数据，同时指明了外部化的信息必须用到的地区。
```java
public interface IContext {

    public Locale getLocale();
    public boolean containsVariable(final String name);
    public Set<String> getVariableNames();
    public Object getVariable(final String name);
    
}
```
There is a specialized extension of this interface, `org.thymeleaf.context.IWebContext`, meant to be used in ServletAPI-based web applications (like SpringMVC).
```java
public interface IWebContext extends IContext {
    
    public HttpServletRequest getRequest();
    public HttpServletResponse getResponse();
    public HttpSession getSession();
    public ServletContext getServletContext();
    
}
```
The Thymeleaf core library offers an implementation of each of these interfaces:

- `org.thymeleaf.context.Context` implements `IContext`
- `org.thymeleaf.context.WebContext` implements `IWebContext`

And as you can see in the controller code, `WebContext` is the one we use. In fact we have to, because the use of a `ServletContextTemplateResolver` requires that we use a context implementing `IWebContext`.
```java
WebContext ctx = new WebContext(request, response, servletContext, request.getLocale());
```
Only three out of those four constructor arguments are required because the default locale for the system will be used if none is specified (although you should never let this happen in real applications).

There are some specialized expressions that we will be able to use to obtain the request parameters and the request, session and application attributes from the `WebContext` in our templates. For example:

- `${x}` will return a variable `x` stored into the Thymeleaf context or as a request attribute.
- `${param.x}` will return a request parameter called `x` (which might be multivalued).
- `${session.x}` will return a session attribute called `x`.
- `${application.x}` will return a servlet context attribute called `x`.