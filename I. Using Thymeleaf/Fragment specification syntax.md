### 片段规范语法

分段表达式的语法相当简单。有三种不同的格式：

- 使用`~{templatename::selector}`包含片段。此片段在名为`templatename`的模版上应用指定的Markup Selector得到。注意：`selector`可以仅仅是一个片段名，所以你可以像上一节里的`~{footer :: copy}`一样，用`~{templatename::fragmentname}`简单地指定片段。

```
Markup Selector语法由底层的AttoParser解析库定义，与XPath表达式或者CSS选择器相似。详细情况请查看[附录C](../I. Using Thymeleaf/20 Appendix C：Markup Selector Syntax.md)。
```

- 使用`~{templatename}`包含名为`templatename`的整个模版。

```
注意：你在`th:insert`/`th:replace`标签里使用的模版名需要能够被模版引擎使用中的模版解析器解析。
```

- 使用`~{::selector}`或者`"~{this::selector}"`，包含同一个模版里匹配`selector`的片段。如果在此表达式出现的模版上找不到相同的选择器，模版调用（insertion）的栈会朝着最初处理的模版（root）遍历，直到在某一级别上匹配到 `selector`。

上面例子里的`templatename`和`selector`可以是完全的表达式（甚至是条件表达式！），比如：
```html
<div th:insert="footer :: (${user.isAdmin}? #{footer.admin} : #{footer.normaluser})"></div>
```

再次注意：在`th:insert`/`th:replaceNote`里可以没有`~{...}`。

片段可以包含任何的`th:*`属性。一旦片段被包含进目标模版（含有`th:insert`/`th:replace`属性），这些属性会被求值，并且它们可以引用定义在目标模版里的任何上下文变量。

```
这种学习片段的方法的好处是你可以在页面上写上你的片段--它们有着完整而且有效的标记结构，能被浏览器完美地表示。同时，可以让Thymeleaf把它们包含进其它模版。
```