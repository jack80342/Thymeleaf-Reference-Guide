### th:assert——用于模板内断言

`th:assert`属性可以指定一个由逗号分隔的表达式列表。各个表达式的值应当为true，否则，引发异常。
```html
<div th:assert="${onevar},(${twovar} != 43)">...</div>
```
这对于片段签名的参数验证很方便：
```html
<header th:fragment="contentheader(title)" th:assert="${!#strings.isEmpty(title)}">...</header>
```