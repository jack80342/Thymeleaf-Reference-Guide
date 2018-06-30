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
如果没有指定这些可解析的模式，我们将依赖每一个正在使用的`ITemplateResolver`实现的特定能力。注意：不是所有的实现能够在解析前知道某个模板是否存在。因此，可以总是认为一个模板是可解析的，并截断解析链（不允许其它解析器检查同一个模板）。但是，之后无法读取真实的资源。

核心Thymeleaf包含的所有`ITemplateResolver`实现包含了一种机制。它允许我们让解析器在认为模板可解析之前检查资源是否存在。It is the `checkExistence` flag, which works like:
```java
ClassLoaderTemplateResolver classLoaderTemplateResolver = new ClassLoaderTemplateResolver();
classLoaderTemplateResolver.setOrder(Integer.valueOf(1));
classLoaderTempalteResolver.setCheckExistence(true);
```
This `checkExistence` flag forces the resolver perform a real check for resource existence during the resolution phase (and let the following resolver in the chain be called if existence check returns false). While this might sound good in every case, in most cases this will mean a double access to the resource itself (once for checking existence, another time for reading it), and could be a performance issue in some scenarios, e.g. remote URL-based template resources – a potential performance issue that might anyway get largely mitigated by the use of the template cache (in which case templates will only be resolved the first time they are accessed).
