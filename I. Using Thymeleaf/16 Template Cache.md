### 16 模版缓存

多亏了一系列的解析器和处理器，Thymeleaf才能够正常工作。解析器用于标记和文本。它将模板解析为事件序列（开始标签、文本、结束标签、注释，等等）。处理器用于每一种需要被应用的行为类型。它修改事件序列，通过合并原始模板与我们的数据，创建期待的结果。

它默认包含缓存。缓存里存储了解析过的模板，以及在处理它们前由于读取和解析模板文件产生的事件序列。当在一个网络应用里工作时，这特别有用。它基于以下观念构建：

- 在任何应用里，输入/输出几乎总是最慢的部分。相较而言，内存里的处理则极其快。
- 克隆一个存在的内存里的事件序列，比读取模板文件、解析它并创建一个新时间序列，要快得多。
- 网络应用通常模板不多。
- 模板文件不大，并且不会在应用运行时被修改。

这说明：在网络应用里缓存最常用的模版是可行的，而且不会浪费大量的内存。同时，也节约了在一小部分实际上从不改变的文件上执行输入/输出操作花费的时间。

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
