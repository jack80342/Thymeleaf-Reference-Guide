### JavaScript自然模版

The mentioned intelligence of the JavaScript inlining mechanism goes much further than just applying JavaScript-specific escaping and outputting expression results as valid literals.

For example, we can wrap our (escaped) inlined expressions in JavaScript comments like:
```html
<script th:inline="javascript">
    ...
    var username = /*[[${session.user.name}]]*/ "Gertrud Kiwifruit";
    ...
</script>
```
And Thymeleaf will ignore everything we have written after the comment and before the semicolon (in this case `'Gertrud Kiwifruit'`), so the result of executing this will look exactly like when we were not using the wrapping comments:
```html
<script th:inline="javascript">
    ...
    var username = "Sebastian \"Fruity\" Applejuice";
    ...
</script>
```
But have another careful look at the original template code:
```html
<script th:inline="javascript">
    ...
    var username = /*[[${session.user.name}]]*/ "Gertrud Kiwifruit";
    ...
</script>
```
Note how this is `valid JavaScript` code. And it will perfectly execute when you open your template file in a static manner (without executing it at a server).

So what we have here is a way to do `JavaScript natural templates`!
