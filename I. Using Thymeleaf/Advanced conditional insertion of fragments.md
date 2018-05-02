### 片段的高级条件插入

The availability of both the emtpy fragment and no-operation token allows us to perform conditional insertion of fragments in a very easy and elegant way.

For example, we could do this in order to insert our `common :: adminhead` fragment only if the user is an administrator, and insert nothing (emtpy fragment) if not:
```html
...
<div th:insert="${user.isAdmin()} ? ~{common :: adminhead} : ~{}">...</div>
...
```
Also, we can use the no-operation token in order to insert a fragment only if the specified condition is met, but leave the markup without modifications if the condition is not met:
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