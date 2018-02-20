### 定义和引用片段

在我们的模版里，我们会时常想要包含来自其它模版的部分，比如页脚、页眉、菜单……

为了这样做，Thymeleaf需要我们定义这些部分——片段，用来包含进其它模版。它可以用`th:fragment`属性定义。

假设，我们想要给所有的杂货店页面添加一个标准的版权页脚。我们创建了`/WEB-INF/templates/footer.html`文件，包含以下代码：
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
上面的代码定义一个叫做`copy`的片段。我们可以使用`th:insert`或者`th:replace`属性（或者`th:include`，尽管在Thymeleaf 3.0之后，不推荐使用它）把它包含进我们的主页：
```html
<body>

  ...

  <div th:insert="~{footer :: copy}"></div>
  
</body>
```
注意：`th:insert`期待一个分段表达式(`~{...}`)。它的求值结果会产生一个片段。在上面的例子里，分段表达式并不复杂。而且，(`~{`,`}`) 封闭是完全可选的，所以上面的代码等价于：
```html
<body>

  ...

  <div th:insert="footer :: copy"></div>
  
</body>
```