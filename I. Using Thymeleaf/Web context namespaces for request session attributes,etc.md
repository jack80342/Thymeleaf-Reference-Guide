### 请求/会话属性的网络上下文命名空间等

当在网络环境下使用Thymeleaf时，我们可以使用一系列的快捷方式访问请求参数、会话属性和应用属性：

```
注意：这些不是上下文对象，而是作为变量被加入到上下文的映射，所以我们不用#访问它们。在某种意义上，它们就像是命名空间。
```

- **param**：用于检索请求参数。`${param.foo}`是一个`String[]`，含有`foo`请求参数的值，所以`${param.foo[0]}`通常用于取得第一个值。  
```java
/*
 * ============================================================================
 * See javadoc API for class org.thymeleaf.context.WebRequestParamsVariablesMap
 * ============================================================================
 */

${param.foo}              // Retrieves a String[] with the values of request parameter 'foo'
${param.size()}
${param.isEmpty()}
${param.containsKey('foo')}
...
```

- **session**：用于检索会话属性。
```java
/*
 * ======================================================================
 * See javadoc API for class org.thymeleaf.context.WebSessionVariablesMap
 * ======================================================================
 */

${session.foo}                 // Retrieves the session atttribute 'foo'
${session.size()}
${session.isEmpty()}
${session.containsKey('foo')}
...
```

- **application**：用于检索应用/servlet上下文属性。
```java
/*
 * =============================================================================
 * See javadoc API for class org.thymeleaf.context.WebServletContextVariablesMap
 * =============================================================================
 */

${application.foo}              // Retrieves the ServletContext atttribute 'foo'
${application.size()}
${application.isEmpty()}
${application.containsKey('foo')}
...
```

**注  不需要为访问请求属性指定一个命名空间**（与请求参数刚好相反），因为所有的请求属性都会被自动地加入上下文，作为上下文根里的变量：
```java
${myRequestAttribute}
```
