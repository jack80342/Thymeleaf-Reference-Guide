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
Additionally, if we have configured our template resolvers to check for existence of the template resources –- by means of their `checkExistence` flag -– we can use the existence of the fragment itself as the condition in a default operation:
```html
...
<!-- The body of the <div> will be used if the "common :: salutation" fragment  -->
<!-- does not exist (or is empty).                                              -->
<div th:insert="~{common :: salutation} ?: _">
    Welcome [[${user.name}]], click <a th:href="@{/support}">here</a> for help-desk support.
</div>
...
```