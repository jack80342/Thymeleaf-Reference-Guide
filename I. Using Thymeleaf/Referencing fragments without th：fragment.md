### 不使用th:fragment引用片段

多亏了强大的Markup Selectors，我们能够在不使用`th:fragment`属性的情况下，包含片段。甚至可以是来自不同应用的标记代码，没有一丁点Thymeleaf的知识：

```html
...
<div id="copy-section">
  &copy; 2011 The Good Thymes Virtual Grocery
</div>
...
```

我们可以通过`id`属性简单地引用上面的片段，类似于CSS选择器：

```html
<body>

  ...

  <div th:insert="~{footer :: #copy-section}"></div>
  
</body>
```