### 使用th:each

对于我们的产品列表页面，我们需要一个控制器方法，来从服务层获得产品列表，并把它添加到模版上下文：
```html
public void process(
        final HttpServletRequest request, final HttpServletResponse response,
        final ServletContext servletContext, final ITemplateEngine templateEngine)
        throws Exception {
    
    ProductService productService = new ProductService();
    List<Product> allProducts = productService.findAll(); 
    
    WebContext ctx = new WebContext(request, response, servletContext, request.getLocale());
    ctx.setVariable("prods", allProducts);
    
    templateEngine.process("product/list", ctx, response.getWriter());
    
}
```
And then we will use th:each in our template to iterate over the list of products:
```html
<!DOCTYPE html>

<html xmlns:th="http://www.thymeleaf.org">

  <head>
    <title>Good Thymes Virtual Grocery</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <link rel="stylesheet" type="text/css" media="all" 
          href="../../../css/gtvg.css" th:href="@{/css/gtvg.css}" />
  </head>

  <body>

    <h1>Product list</h1>
  
    <table>
      <tr>
        <th>NAME</th>
        <th>PRICE</th>
        <th>IN STOCK</th>
      </tr>
      <tr th:each="prod : ${prods}">
        <td th:text="${prod.name}">Onions</td>
        <td th:text="${prod.price}">2.41</td>
        <td th:text="${prod.inStock}? #{true} : #{false}">yes</td>
      </tr>
    </table>
  
    <p>
      <a href="../home.html" th:href="@{/}">Return to home</a>
    </p>

  </body>

</html>
```
That `prod : ${prods}` attribute value you see above means “for each element in the result of evaluating `${prods}`, repeat this fragment of template, using the current element in a variable called prod”. Let’s give a name each of the things we see:

- We will call `${prods}` the iterated expression or iterated variable.
- We will call `prod` the iteration variable or simply iter variable.

Note that the `prod` iter variable is scoped to the `<tr>` element, which means it is available to inner tags like `<td>`.