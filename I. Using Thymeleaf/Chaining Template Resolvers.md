### 链接模板解析器

模板引擎可以指定多个模板解析器。这种情况下，可以指定解析的先后顺序。这样，如果第一个解析器无法解析模板，就会去请求第二个：
```java
ClassLoaderTemplateResolver classLoaderTemplateResolver = new ClassLoaderTemplateResolver();
classLoaderTemplateResolver.setOrder(Integer.valueOf(1));

ServletContextTemplateResolver servletContextTemplateResolver = 
        new ServletContextTemplateResolver(servletContext);
servletContextTemplateResolver.setOrder(Integer.valueOf(2));

templateEngine.addTemplateResolver(classLoaderTemplateResolver);
templateEngine.addTemplateResolver(servletContextTemplateResolver);
```
当应用了多个模板解析器时，推荐为每个模板解析器指定模式。这样，Thymeleaf能够快速取消那些无法解析模板的模板解析器，增强性能。这并不是强制性的，但推荐这样做。
```java
ClassLoaderTemplateResolver classLoaderTemplateResolver = new ClassLoaderTemplateResolver();
classLoaderTemplateResolver.setOrder(Integer.valueOf(1));
// This classloader will not be even asked for any templates not matching these patterns 
classLoaderTemplateResolver.getResolvablePatternSpec().addPattern("/layout/*.html");
classLoaderTemplateResolver.getResolvablePatternSpec().addPattern("/menu/*.html");

ServletContextTemplateResolver servletContextTemplateResolver = 
        new ServletContextTemplateResolver(servletContext);
servletContextTemplateResolver.setOrder(Integer.valueOf(2));
```
如果没有指定这些可解析的模式，我们将依赖每一个正在使用的`ITemplateResolver`实现的特定能力。注意：不是所有的实现都能够在解析前知道某个模板是否存在。因此，可以总是认为一个模板是可解析的，并截断解析链（不允许其它解析器检查同一个模板）。但是，之后无法读取真实的资源。

核心Thymeleaf包含的所有`ITemplateResolver`实现包含了一种机制。它允许我们让解析器在认为模板可解析之前检查资源是否存在。也就是`checkExistence`标志，比如：
```java
ClassLoaderTemplateResolver classLoaderTemplateResolver = new ClassLoaderTemplateResolver();
classLoaderTemplateResolver.setOrder(Integer.valueOf(1));
classLoaderTempalteResolver.setCheckExistence(true);
```
这个`checkExistence`标志强制解析器检查在解析阶段资源是否存在（如果返回false，则会调用链里的下一个解析器）。在每一种情况下，这可能听起来感觉不错。在大多数情况下，这意味着会访问资源两次（一次检查是否存在，另一次读取它）。在某些场景下，这会是一个性能问题，比如：基于远程URL的模板资源————这个潜在的问题可以通过使用模板缓存极大地缓解（这种情况下，模板只会在第一次访问的时候被解析）。
