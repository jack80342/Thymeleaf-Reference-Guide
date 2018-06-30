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
If these resolvable patterns are not specified, we will be relying on the specific capabilities of each of the `ITemplateResolver` implementations we are using. Note that not all implementations might be able to determine the existence of a template before resolving, and thus could always consider a template as resolvable and break the resolution chain (not allowing other resolvers to check for the same template), but then be unable to read the real resource.

All the `ITemplateResolver` implementations that are included with core Thymeleaf include a mechanism that will allow us to make the resolvers really check if a resource exists before considering it resolvable. It is the `checkExistence` flag, which works like:
```java
ClassLoaderTemplateResolver classLoaderTemplateResolver = new ClassLoaderTemplateResolver();
classLoaderTemplateResolver.setOrder(Integer.valueOf(1));
classLoaderTempalteResolver.setCheckExistence(true);
```
This `checkExistence` flag forces the resolver perform a real check for resource existence during the resolution phase (and let the following resolver in the chain be called if existence check returns false). While this might sound good in every case, in most cases this will mean a double access to the resource itself (once for checking existence, another time for reading it), and could be a performance issue in some scenarios, e.g. remote URL-based template resources – a potential performance issue that might anyway get largely mitigated by the use of the template cache (in which case templates will only be resolved the first time they are accessed).
