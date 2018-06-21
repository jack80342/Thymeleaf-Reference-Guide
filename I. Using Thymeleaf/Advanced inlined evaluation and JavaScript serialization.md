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
The way this JavaScript serialization is done is by means of an implementation of the `org.thymeleaf.standard.serializer.IStandardJavaScriptSerializer` interface, which can be configured at the instance of the `StandardDialect` being used at the template engine.

The default implementation of this JS serialization mechanism will look for the [Jackson library](https://github.com/FasterXML/jackson) in the classpath and, if present, will use it. If not, it will apply a built-in serialization mechanism that covers the needs of most scenarios and produces similar results (but is less flexible).