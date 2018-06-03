### 9 本地变量

Thymeleaf把定义在特定的模版片段里，只在那个片段里才有效的变量，称为本地变量。

我们已经看过一个例子，在产品列表页面的`prod`遍历变量：
```html
<tr th:each="prod : ${prods}">
    ...
</tr>
```
那个`prod`变量只在`<tr>`标签里才有效。特别的：

- 对在那个标签里执行的优先级低于`th:each`（也就是说它们将在`th:each`之后执行）的任何其它的`th:*`属性有效。
- 对`<tr>`标签的任何子元素有效，比如`<td>`元素。

Thymeleaf提供了一种不使用遍历声明本地变量的方法————使用`th:with`属性，它的语法类似于属性值赋值：
```html
<div th:with="firstPer=${persons[0]}">
  <p>
    The name of the first person is <span th:text="${firstPer.name}">Julius Caesar</span>.
  </p>
</div>
```
当`th:with`被处理，`firstPer`变量会被创建为一个本地变量，并加入到上下文的变量映射关系里。这样，它就和其它定义在上下文里的变量一样，能够求值，但只限于包含它的`<div>`标签里面。

你可以使用通常的多重赋值语法，同时定义多个变量：
```html
<div th:with="firstPer=${persons[0]},secondPer=${persons[1]}">
  <p>
    The name of the first person is <span th:text="${firstPer.name}">Julius Caesar</span>.
  </p>
  <p>
    But the name of the second person is 
    <span th:text="${secondPer.name}">Marcus Antonius</span>.
  </p>
</div>
```
`th:with`属性允许重用定义在同一个属性里的变量：
```html
<div th:with="company=${user.company + ' Co.'},account=${accounts[company]}">...</div>
```
让我们在杂货店的主页上使用一下！还记得我们用来格式化输入日期的代码吗？
```html
<p>
  Today is: 
  <span th:text="${#calendars.format(today,'dd MMMM yyyy')}">13 february 2011</span>
</p>
```
如果我们想要`"dd MMMM yyyy"`实际上依赖本地化设置呢？比如，我们可能想要在`home_en.properties`里添加以下信息：
```properties
date.format=MMMM dd'','' yyyy
```
等价于我们的`home_es.properties`：
```properties
date.format=dd ''de'' MMMM'','' yyyy
```
现在，让我们使用`th:with`把本地化的日期格式放进变量里，然后在我们的`th:text`表达式里使用它：
```html
<p th:with="df=#{date.format}">
  Today is: <span th:text="${#calendars.format(today,df)}">13 February 2011</span>
</p>
```
这就干净简单多了。实际上，`th:with`的`优先级`高于`th:text`。我们可以使用`span`标签解决：
```html
<p>
  Today is: 
  <span th:with="df=#{date.format}" 
        th:text="${#calendars.format(today,df)}">13 February 2011</span>
</p>
```
你可能正在想：优先级是上面🤔？我们还没有讨论过它！不过，别担心，下一章讲的就是它。
