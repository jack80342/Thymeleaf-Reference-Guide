### 启用解耦的模版

默认的，并不是每一个模板都需要解耦的逻辑。配置好的模板解析器（`ITemplateResolver`的实现）需要明确地标记出使用解耦的逻辑的模板。

除了`StringTemplateResolver`（它不允许解耦的逻辑），所有其它的`ITemplateResolver`的开箱即用的实现提供了一个叫做`useDecoupledLogic`的标记。 that will mark all templates resolved by that resolver as potentially having all or part of its logic living in a separate resource:
```java
final ServletContextTemplateResolver templateResolver = 
        new ServletContextTemplateResolver(servletContext);
...
templateResolver.setUseDecoupledLogic(true);
```
