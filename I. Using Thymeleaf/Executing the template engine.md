### 执行模版引擎

With our context object ready, now we can tell the template engine to process the template (by its name) using the context, and passing it a response writer so that the response can be written to it:
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