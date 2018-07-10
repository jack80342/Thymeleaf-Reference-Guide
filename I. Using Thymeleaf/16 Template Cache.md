### 16 模版缓存

多亏了一系列的解析器和处理器，Thymeleaf才能够正常工作。解析器用于标记和文本。它将模板解析为事件序列（开始标签、文本、结束标签、注释，等等）。处理器用于每一种需要被应用的行为类型。它修改事件序列，通过合并原始模板与我们的数据，创建期待的结果。

It also includes – by default – a cache that stores parsed templates; the sequence of events resulting from reading and parsing template files before processing them. This is especially useful when working in a web application, and builds on the following concepts:

- Input/Output is almost always the slowest part of any application. In-memory processing is extremely quick by comparison.
- Cloning an existing in-memory event sequence is always much quicker than reading a template file, parsing it and creating a new event sequence for it.
- Web applications usually have only a few dozen templates.
- Template files are small-to-medium size, and they are not modified while the application is running.

This all leads to the idea that caching the most used templates in a web application is feasible without wasting large amounts of memory, and also that it will save a lot of time that would be spent on input/output operations on a small set of files that, in fact, never change.

And how can we take control of this cache? First, we’ve learned before that we can enable or disable it at the Template Resolver, even acting only on specific templates:
```java
// Default is true
templateResolver.setCacheable(false);
templateResolver.getCacheablePatternSpec().addPattern("/users/*");
```
Also, we could modify its configuration by establishing our own Cache Manager object, which could be an instance of the default `StandardCacheManager` implementation:
```java
// Default is 200
StandardCacheManager cacheManager = new StandardCacheManager();
cacheManager.setTemplateCacheMaxSize(100);
...
templateEngine.setCacheManager(cacheManager);
```
Refer to the javadoc API of `org.thymeleaf.cache.StandardCacheManager` for more info on configuring the caches.

Entries can be manually removed from the template cache:
```java
// Clear the cache completely
templateEngine.clearTemplateCache();

// Clear a specific template from the cache
templateEngine.clearTemplateCacheFor("/users/userList");
```
