### 高级特性：CSS自然模版等

与之前介绍的JavaScript内联实现自然模版的方式相同，CSS内联也允许我们的`<style>标签`静态或者动态地工作。也就是说，通过在注释里包装内联表达式实现`CSS自然模版`。请看：
```html
<style th:inline="css">
    .main\ elems {
      text-align: /*[[${align}]]*/ left;
    }
</style>
```