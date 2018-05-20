### 9 本地变量

Thymeleaf calls local variables the variables that are defined for a specific fragment of a template, and are only available for evaluation inside that fragment.

An example we have already seen is the `prod` iter variable in our product list page:
```html
<tr th:each="prod : ${prods}">
    ...
</tr>
```
That `prod` variable will be available only within the bounds of the `<tr>` tag. Specifically:

- It will be available for any other `th:*` attributes executing in that tag with less precedence than `th:each` (which means they will execute after `th:each`).
- It will be available for any child element of the `<tr>` tag, such as any `<td>` elements.

Thymeleaf offers you a way to declare local variables without iteration, using the `th:with` attribute, and its syntax is like that of attribute value assignments:
```html
<div th:with="firstPer=${persons[0]}">
  <p>
    The name of the first person is <span th:text="${firstPer.name}">Julius Caesar</span>.
  </p>
</div>
```
When `th:with` is processed, that `firstPer` variable is created as a local variable and added to the variables map coming from the context, so that it is available for evaluation along with any other variables declared in the context, but only within the bounds of the containing `<div>` tag.

You can define several variables at the same time using the usual multiple assignment syntax:
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
The `th:with` attribute allows reusing variables defined in the same attribute:
```html
<div th:with="company=${user.company + ' Co.'},account=${accounts[company]}">...</div>
```
Let’s use this in our Grocery’s home page! Remember the code we wrote for outputting a formatted date?
```html
<p>
  Today is: 
  <span th:text="${#calendars.format(today,'dd MMMM yyyy')}">13 february 2011</span>
</p>
```
Well, what if we wanted that `"dd MMMM yyyy"` to actually depend on the locale? For example, we might want to add the following message to our `home_en.properties`:
```properties
date.format=MMMM dd'','' yyyy
```
…and an equivalent one to our `home_es.properties`:
```properties
date.format=dd ''de'' MMMM'','' yyyy
```
Now, let’s use `th:with` to get the localized date format into a variable, and then use it in our `th:text` expression:
```html
<p th:with="df=#{date.format}">
  Today is: <span th:text="${#calendars.format(today,df)}">13 February 2011</span>
</p>
```
That was clean and easy. In fact, given the fact that `th:with` has a higher `precedence` than `th:text`, we could have solved this all in the `span` tag:
```html
<p>
  Today is: 
  <span th:with="df=#{date.format}" 
        th:text="${#calendars.format(today,df)}">13 February 2011</span>
</p>
```
You might be thinking: Precedence? We haven’t talked about that yet! Well, don’t worry because that is exactly what the next chapter is about.