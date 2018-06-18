### 禁用内联

这个机制可以被禁用。因为确实会有场合，我们想要输出`[[...]]`或者`[(...)]`序列，而不想让它的内容被作为表达式处理。这种情况下，我们将会使用`th:inline="none"`：
```html
<p th:inline="none">A double array looks like this: [[1, 2, 3], [4, 5]]!</p>
```
这会输出：
```html
<p>A double array looks like this: [[1, 2, 3], [4, 5]]!</p>
```