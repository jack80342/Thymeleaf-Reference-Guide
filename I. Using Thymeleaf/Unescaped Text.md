### 非转义文本

The simplest version of our Home page seems to be ready now, but there is something we have not thought about… what if we had a message like this?
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