### 标准信息解析器

So how does `StandardMessageResolver` look for the messages requested at a specific template?

If the template name is `home` and it is located in `/WEB-INF/templates/home.html`, and the requested locale is `gl_ES` then this resolver will look for messages in the following files, in this order:

- `/WEB-INF/templates/home_gl_ES.properties`
- `/WEB-INF/templates/home_gl.properties`
- `/WEB-INF/templates/home.properties`

Refer to the JavaDoc documentation of the `StandardMessageResolver` class for more detail on how the complete message resolution mechanism works.