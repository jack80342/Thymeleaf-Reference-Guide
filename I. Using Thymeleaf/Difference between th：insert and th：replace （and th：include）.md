### th:insert与th:replace（与th:include）的区别

`th:insert`与`th:replace` （与`th:include`，从3.0开始不推荐使用）的区别是什么呢？

- `th:insert`是最简单的：它会简单地把指定的片段作为它的宿主标签的主体插入。

- `th:replace`实际上用指定的段落取代它的宿主标签。

- `th:include`类似于`th:insert`，但是不是插入片段，而是仅仅插入片段的内容。

所以，如下的HTML片段：
```html
<footer th:fragment="copy">
  &copy; 2011 The Good Thymes Virtual Grocery
</footer>
```
像这样，在宿主`<div>`标签里被包含了三次：
```html
<body>

  ...

  <div th:insert="footer :: copy"></div>

  <div th:replace="footer :: copy"></div>

  <div th:include="footer :: copy"></div>

</body>
```
会生成：
```html
<body>

  ...

  <div>
    <footer>
      &copy; 2011 The Good Thymes Virtual Grocery
    </footer>
  </div>

  <footer>
    &copy; 2011 The Good Thymes Virtual Grocery
  </footer>

  <div>
    &copy; 2011 The Good Thymes Virtual Grocery
  </div>
```