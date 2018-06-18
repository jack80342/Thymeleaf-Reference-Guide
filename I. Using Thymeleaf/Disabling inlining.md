### 禁用内联

This mechanism can be disabled though, because there might actually be occasions in which we do want to output the `[[...]]` or `[(...)]` sequences without its contents being processed as an expression. For that, we will use `th:inline="none"`:
```html
<p th:inline="none">A double array looks like this: [[1, 2, 3], [4, 5]]!</p>
```
This will result in:
```html
<p>A double array looks like this: [[1, 2, 3], [4, 5]]!</p>
```