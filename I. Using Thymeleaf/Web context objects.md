### 网络上下文对象

在网络环境下，如下对象可以直接访问（注意：它们是对象，不是映射或者命名空间）：

- **#request **：直接访问与当前请求相关联的`javax.servlet.http.HttpServletRequest`对象。
```java
${#request.getAttribute('foo')}
${#request.getParameter('foo')}
${#request.getContextPath()}
${#request.getRequestName()}
...
```

- **#session **：直接访问与当前请求相关联的`javax.servlet.http.HttpSession`对象。
```java
${#session.getAttribute('foo')}
${#session.id}
${#session.lastAccessedTime}
...
```

- **#servletContext**：直接访问与当前请求相关联的`javax.servlet.ServletContext`对象。
```java
${#servletContext.getAttribute('foo')}
${#servletContext.contextPath}
...
```

