### 布尔字面量

布尔字面量是`true`和`false`。比如：
```html
<div th:if="${user.isAdmin()} == false"> ...
```
在这个例子里，`== false`写在了花括号的外面，所以Thymeleaf会照看它。如果它写在花括号里面，就由OGNL/SpringEL引擎负责：
```html
<div th:if="${user.isAdmin() == false}"> ...
```