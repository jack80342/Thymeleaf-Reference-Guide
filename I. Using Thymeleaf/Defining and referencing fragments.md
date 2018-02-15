### 定义和引用片段

在我们的模版里，我们会时常想要包含来自其它模版的部分，比如页脚、页眉、菜单……

为了这样做，Thymeleaf需要我们定义这些部分——片段，用来包含进其它模版。它可以用`th:fragment`属性定义。

Say we want to add a standard copyright footer to all our grocery pages, so we create a `/WEB-INF/templates/footer.html` file containing this code:
```html
<!DOCTYPE html>

<html xmlns:th="http://www.thymeleaf.org">

  <body>
  
    <div th:fragment="copy">
      &copy; 2011 The Good Thymes Virtual Grocery
    </div>
  
  </body>
  
</html>
```
The code above defines a fragment called `copy` that we can easily include in our home page using one of the `th:insert` or `th:replace` attributes (and also `th:include`, though its use is no longer recommended since Thymeleaf 3.0):
```html
<body>

  ...

  <div th:insert="~{footer :: copy}"></div>
  
</body>
```
Note that `th:insert` expects a fragment expression (`~{...}`), which is an expression that results in a fragment. In the above example though, which is a non-complex fragment expression, the (`~{`,`}`) enclosing is completely optional, so the code above would be equivalent to:
```html
<body>

  ...

  <div th:insert="footer :: copy"></div>
  
</body>
```