### 非转义文本

现在，Home页面的最简单版本看起来已经准备就绪了，但是还有一些我们没有考虑到的情况……要是，我们有这样的一段信息，改怎么办呢？
```html
home.welcome=Welcome to our <b>fantastic</b> grocery store!
```
如果我们像之前一样执行模版，将会得到：
```html
<p>Welcome to our &lt;b&gt;fantastic&lt;/b&gt; grocery store!</p>
```
这并不是我们期望的结果，因为`<b>`标签已经被转义了，所以浏览器里才会这样显示。

这是`th:text`属性的默认行为。如果我们想要Thymeleaf尊重我们的HTML标签不去转义它们，我们需要使用另一个不同的标签：`th:utext`。
```html
<p th:utext="#{home.welcome}">Welcome to our grocery store!</p>
```
这将会同我们想要的那样，输出我们的信息：
```html
<p>Welcome to our <b>fantastic</b> grocery store!</p>
```