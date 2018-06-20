### JavaScript自然模版

之前提及的 JavaScript内联机制的智能，远不止应用JavaScript特定的转义和以有效的字面量输出表达式结果。

比如，我们可以在JavaScript注释里包装我们的（转义的）内联表达式：
```html
<script th:inline="javascript">
    ...
    var username = /*[[${session.user.name}]]*/ "Gertrud Kiwifruit";
    ...
</script>
```
Thymeleaf会忽略所有写在注释后面分号前面的东西（这里是`'Gertrud Kiwifruit'`），所以执行的结果会和没有使用包装的注释的情况一样：
```html
<script th:inline="javascript">
    ...
    var username = "Sebastian \"Fruity\" Applejuice";
    ...
</script>
```
但是，再仔细看一下原始的模版代码：
```html
<script th:inline="javascript">
    ...
    var username = /*[[${session.user.name}]]*/ "Gertrud Kiwifruit";
    ...
</script>
```
注意：这是`有效的JavaScript`代码。当你静态地打开你的模版文件（不在服务器上执行）时，它也将完美的执行。

所以，这儿讲的就是一种实现`JavaScript自然模版`的方式！