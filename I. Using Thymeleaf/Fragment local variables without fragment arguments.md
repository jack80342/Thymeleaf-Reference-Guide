### 不带片段参数的片段本地变量

即使片段定义的时候不带参数，就像这样：
```html
<div th:fragment="frag">
    ...
</div>
```
我们可以用上面提到的第二种语法调用它们（而且只能使用第二种）：
```html
<div th:replace="::frag (onevar=${value1},twovar=${value2})">
```
这相当于结合了`th:replace`和`th:with`：
```html
<div th:replace="::frag" th:with="onevar=${value1},twovar=${value2}">
```
**注意** 这种为片段指定本地变量的方法——不管有没有参数签名，不会使得上下文在执行前变为空。片段还是可以访问每一个正在调用的模版里正在被使用的上下文变量。