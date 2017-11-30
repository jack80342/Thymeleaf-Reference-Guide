### 模版引擎

模版引擎对象实现了`org.thymeleaf.ITemplateEngine`接口。这些实现里的一个由Thymeleaf核心提供：`org.thymeleaf.TemplateEngine`。我们在这儿创建了一个它的实例：
```java
templateEngine = new TemplateEngine();
templateEngine.setTemplateResolver(templateResolver);
```
相当简单，不是嘛？我们要做的就是创建一个实例，并设置模板解析器。

模板解析器是`模版引擎`唯一需要的参数。虽然之后还有许多其它的东西（消息解析器、缓存大小，等等）要涉及，但是目前来说，这就是我们需要的全部东西了。

现在，我们的模版引擎已经准备就绪，我们可以开始使用Thymeleaf创建网页了。