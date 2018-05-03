### 片段的高级条件插入

空片段和无操作标记允许我们以一种非常简单优雅的方式执行片段的条件插入。

例如，为了只在用户是管理员的时候，才插入我们的`common :: adminhead`片段。不是管理员的时候，不插入（空片段）。我们可以这样写：
```html
...
<div th:insert="${user.isAdmin()} ? ~{common :: adminhead} : ~{}">...</div>
...
```
另外，为了只在特定条件满足时插入片段，在条件不满足时不修改标记，我们可以使用无操作标记：
```html
...
<div th:insert="${user.isAdmin()} ? ~{common :: adminhead} : _">
    Welcome [[${user.name}]], click <a th:href="@{/support}">here</a> for help-desk support.
</div>
...
```
此外，如果我们已经配置好模版解析器检查模版资源是否存在——依据`checkExistence`标记，我们可以把片段自身存在与否用作默认操作的条件：
```html
...
<!-- The body of the <div> will be used if the "common :: salutation" fragment  -->
<!-- does not exist (or is empty).                                              -->
<div th:insert="~{common :: salutation} ?: _">
    Welcome [[${user.name}]], click <a th:href="@{/support}">here</a> for help-desk support.
</div>
...
```