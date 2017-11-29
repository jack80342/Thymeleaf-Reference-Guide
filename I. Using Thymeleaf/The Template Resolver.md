### 模版解析器

让我们从模版解析器开始：
```java
ServletContextTemplateResolver templateResolver = 
        new ServletContextTemplateResolver(servletContext);
```
模版解析器是一些对象。这些对象实现了来自于Thymeleaf API的接口（`org.thymeleaf.templateresolver.ITemplateResolver`）：
```java
public interface ITemplateResolver {

    ...
  
    /*
     * Templates are resolved by their name (or content) and also (optionally) their 
     * owner template in case we are trying to resolve a fragment for another template.
     * Will return null if template cannot be handled by this template resolver.
     */
    public TemplateResolution resolveTemplate(
            final IEngineConfiguration configuration,
            final String ownerTemplate, final String template,
            final Map<String, Object> templateResolutionAttributes);
}
```
这些对象决定着我们的模版怎样被访问。在百里香虚拟杂货店应用里，`org.thymeleaf.templateresolver.ServletContextTemplateResolver`意味着：我们将会把模版文件作为来自于Servlet上下文的资源来取回。应用范围的`javax.servlet.ServletContext`对象存在于每一个Java网络应用。它会从网络应用根部分解资源。

但是，这并不是我们能够讨论的关于模版解析器的所有内容，因为我们能够在它上面设置一些配置参数。首先，模版模式：
```java
templateResolver.setTemplateMode(TemplateMode.HTML);
```
HTML是`ServletContextTemplateResolver`默认的模版模式，但是多写上这一行是一种良好的实践，这样对于将要发生什么，看到我们的代码就会一目了然。
```java
templateResolver.setPrefix("/WEB-INF/templates/");
templateResolver.setSuffix(".html");
```
前缀和后缀会修改我们传递给引擎的模版名字。

使用这项配置，模版名“product/list”会变成：
```java
servletContext.getResourceAsStream("/WEB-INF/templates/product/list.html")
```
🉑️选地，通过设置`cacheTTLMs`属性，可以在模版解析器里配置解析好的模版在缓存里的存活时间。
```java
templateResolver.setCacheTTLMs(3600000L);
```
如果达到了最大缓存，并且还是目前最旧的入口，那么在生存时间结束之前，模版仍旧会从缓存中被除去。
```
用户可以通过实现`ICacheManager`接口，来定义缓存的行为和大小，或者修改`StandardCacheManager`对象来管理默认的缓存。
```
模版解析器还有很多要学习的地方，但是目前让我们先看一看模版引擎对象的创建方法。