### 上下文

In order to process our template, we will create a `HomeController` class implementing the `IGTVGController` interface we saw before:
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
The first thing we see is the creation of a context. A Thymeleaf context is an object implementing the `org.thymeleaf.context.IContext` interface. Contexts should contain all the data required for an execution of the template engine in a variables map, and also reference the locale that must be used for externalized messages.
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