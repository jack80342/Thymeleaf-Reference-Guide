### 高级特性：CSS自然模版等

In an equivalent way to what was explained before for JavaScript, CSS inlining also allows for our `<style>` tags to work both statically and dynamically, i.e. as `CSS natural templates` by means of wrapping inlined expressions in comments. See:
```html
<style th:inline="css">
    .main\ elems {
      text-align: /*[[${align}]]*/ left;
    }
</style>
```