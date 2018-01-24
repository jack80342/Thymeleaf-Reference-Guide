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
然后，我们在我们的模版里使用th:each来遍历产品列表：
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
你在上面看到的那个`prod : ${prods}`属性值的意思是“对于求值`${prods}`结果里的每一个元素，重复这段模版，在一个叫作prod的变量里使用当前的元素”。让我们给看到的每一个东西取一个名字：

- 我们把`${prods}`称为被遍历表达式或者被遍历变量。
- 我们把`prod`称为遍历变量。

需要注意`prod`遍历变量的作用范围是`<tr>`元素，这意味着可以使用内部标签，像`<td>`。