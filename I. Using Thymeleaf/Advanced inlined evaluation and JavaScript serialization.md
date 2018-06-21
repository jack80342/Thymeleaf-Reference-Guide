### 高级内联求值与JavaScript序列化

关于JavaScript内联有一件重要的事情需要提醒一下：它的表达式求值是智能的，不限于Strings。Thymeleaf会用JavaScript语法正确地书写下列类别地对象：

- Strings
- Numbers
- Booleans
- Arrays
- Collections
- Maps
- Beans (objects with getter and setter methods)

比如，如果我们有下列代码：
```html
<script th:inline="javascript">
    ...
    var user = /*[[${session.user}]]*/ null;
    ...
</script>
```
`${session.user}`表达式会求值为`User`对象，并且Thymeleaf将会把它正确地转化为Javascript语法：
```html
<script th:inline="javascript">
    ...
    var user = {"age":null,"firstName":"John","lastName":"Apricot",
                "name":"John Apricot","nationality":"Antarctica"};
    ...
</script>
```
这种JavaScript序列化通过`org.thymeleaf.standard.serializer.IStandardJavaScriptSerializer`接口实现。它可以在模版引擎使用的`StandardDialect`实例里配置。

这个JS序列化机制的默认实现将会在类路径里寻找[Jackson library](https://github.com/FasterXML/jackson)。如果存在，就使用它。否则，它将会应用内建的序列化机制，来满足大部分场景下的需求，并产生相似的结果（但更不灵活）。