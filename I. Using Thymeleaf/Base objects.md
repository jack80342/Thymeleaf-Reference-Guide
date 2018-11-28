### 基本对象

- **#ctx**: 上下文对象。`org.thymeleaf.context.IContext`或是`org.thymeleaf.context.IWebContext`的实现，取决于我们的环境（单独的应用或者网络应用）。

注意：`#vars`和`#root`是它的同义词，但是推荐使用`#ctx`。

```java
/*
 * ======================================================================
 * See javadoc API for class org.thymeleaf.context.IContext
 * ======================================================================
 */

${#ctx.locale}
${#ctx.variableNames}

/*
 * ======================================================================
 * See javadoc API for class org.thymeleaf.context.IWebContext
 * ======================================================================
 */

${#ctx.request}
${#ctx.response}
${#ctx.session}
${#ctx.servletContext}
```
- **#locale** : 直接访问当前请求关联的`java.util.Locale`。

```java
${#locale}
```