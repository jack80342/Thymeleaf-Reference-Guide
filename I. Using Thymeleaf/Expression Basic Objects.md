### 表达式基本对象

When evaluating OGNL expressions on the context variables, some objects are made available to expressions for higher flexibility. These objects will be referenced (per OGNL standard) starting with the `#` symbol:

`#ctx`: the context object.
`#vars`: the context variables.
`#locale`: the context locale.
`#request`: (only in Web Contexts) the `HttpServletRequest` object.
`#response`: (only in Web Contexts) the `HttpServletResponse` object.
`#session`: (only in Web Contexts) the `HttpSession` object.
`#servletContext`: (only in Web Contexts) the `ServletContext` object.
So we can do this:
```html
Established locale country: <span th:text="${#locale.country}">US</span>.
```
You can read the full reference of these objects in [Appendix A](http://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#appendix-a-expression-basic-objects).