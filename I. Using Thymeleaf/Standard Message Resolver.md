### 标准信息解析器

那么，`StandardMessageResolver`是怎么寻找在特定模版里请求的信息的呢？

如果模版名字是`home`，位置是`/WEB-INF/templates/home.html`，并且请求的区域信息是`gl_ES`，那么解析器会在下列文件里以如下顺序寻找信息：

- `/WEB-INF/templates/home_gl_ES.properties`
- `/WEB-INF/templates/home_gl.properties`
- `/WEB-INF/templates/home.properties`

完整的信息解析机制，请参考`StandardMessageResolver`类的JavaDoc文档。