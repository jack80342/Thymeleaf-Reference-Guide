### 表达式基本对象

当在上下文变量上，对OGNL表达式求值时，一些对象对表达式具有更高的灵活性。这些对象通过`#`符号引用。

- `#ctx`: 上下文对象
- `#vars`: 上下文变量
- `#locale`: 上下文地区
- `#request`: （只在Web上下文里）`HttpServletRequest`对象
- `#response`: （只在Web上下文里）`HttpServletResponse`对象
- `#session`: （只在Web上下文里）`HttpSession`对象
- `#servletContext`: （只在Web上下文里）`ServletContext`对象

所以，我们可以这么做：
```html
Established locale country: <span th:text="${#locale.country}">US</span>.
```
你可以在[附录 A](http://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#appendix-a-expression-basic-objects)里阅读这些对象的完整说明。