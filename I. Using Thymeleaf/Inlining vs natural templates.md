### 内联对战自然模版

If you come from other template engines in which this way of outputting text is the norm, you might be asking: Why aren’t we doing this from the beginning? It’s less code than all those `th:text` attributes!

Well, be careful there, because although you might find inlining quite interesting, you should always remember that inlined expressions will be displayed verbatim in your HTML files when you open them statically, so you probably won’t be able to use them as design prototypes anymore!

The difference between how a browser would statically display our fragment of code without using inlining…
```html
Hello, Sebastian!
```
…and using it…
```html
Hello, [[${session.user.name}]]!
```
…is quite clear in terms of design usefulness.