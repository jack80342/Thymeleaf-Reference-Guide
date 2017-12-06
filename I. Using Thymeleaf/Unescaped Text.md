### 非转义文本

现在，Home页面的最简单版本看起来已经准备就绪了，但是还有一些我们没有考虑到的情况……要是，我们有这样的一段信息，改怎么办呢？
```html
home.welcome=Welcome to our <b>fantastic</b> grocery store!
```
If we execute this template like before, we will obtain:
```html
<p>Welcome to our &lt;b&gt;fantastic&lt;/b&gt; grocery store!</p>
```
Which is not exactly what we expected, because our `<b>` tag has been escaped and therefore it will be displayed in the browser.

This is the default behaviour of the `th:text` attribute. If we want Thymeleaf to respect our HTML tags and not escape them, we will have to use a different attribute: `th:utext` (for “unescaped text”):
```html
<p th:utext="#{home.welcome}">Welcome to our grocery store!</p>
```
This will output our message just like we wanted it:
```html
<p>Welcome to our <b>fantastic</b> grocery store!</p>
```