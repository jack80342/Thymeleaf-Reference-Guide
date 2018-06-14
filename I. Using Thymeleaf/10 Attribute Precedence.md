### 10 属性优先级

当你在同一个标签里，写上多个`th:*`属性时，会发生什么🤔呢？ 比如：
```html
<ul>
  <li th:each="item : ${items}" th:text="${item.description}">Item description here...</li>
</ul>
```
我们会期待`th:each`属性在`th:text`之前执行。这样，我们就能得到想要的结果。但是，实际上HTML/XML标准并没有任何关于标签里属性执行顺序的规定。为了确保在这样的情况下按预期方式工作，我们需要建立一种属性的优先级机制。

所以，所有Thymeleaf的属性定义了数字上的优先级。这样就解决了标签里属性执行顺序的问题。顺序如下：

|顺序|特性|属性|
|---|---|---|
|1|包含片段|th:insert<br/>th:replace|
|2|遍历片段|th:each|
|3|条件求值|th:if<br/>th:unless<br/>th:switch<br/>th:case|
|4|定义本地变量|th:object<br/>th:with|
|5|修改通用属性|th:attr<br/>th:attrprepend<br/>th:attrappend|
|6|修改特定属性|th:value<br/>th:href<br/>th:src<br/>······|
|7|文本（修改标签主体）|th:text<br/>th:utext|
|8|指定片段|th:fragment|
|9|移除片段|th:remove|

这种优先级机制意味着：如果颠倒属性的位置（尽管可读性会稍微变差），上面的片段遍历也会得到完全相同的结果：
```html
<ul>
  <li th:text="${item.description}" th:each="item : ${items}">Item description here...</li>
</ul>
```