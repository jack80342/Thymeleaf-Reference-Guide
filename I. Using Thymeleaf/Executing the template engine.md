### 执行模版引擎

我们的上下文对象已经准备好了，现在我们可以让模版引擎处理模版了（通过名字）。使用上下文，同时传给它一个response writer，这样就能把response写入到它里面：
```java
templateEngine.process("home", ctx, response.getWriter());
```
Let’s see the results of this using the Spanish locale:
```html
<!DOCTYPE html>

<html>

  <head>
    <title>Good Thymes Virtual Grocery</title>
    <meta content="text/html; charset=UTF-8" http-equiv="Content-Type"/>
    <link rel="stylesheet" type="text/css" media="all" href="/gtvg/css/gtvg.css" />
  </head>

  <body>
  
    <p>¡Bienvenido a nuestra tienda de comestibles!</p>

  </body>

</html>
```