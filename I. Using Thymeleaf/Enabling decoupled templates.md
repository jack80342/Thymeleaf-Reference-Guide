### 启用解耦的模版

Decoupled logic will not be expected for every template by default. Instead, the configured template resolvers (implementations of `ITemplateResolver`) will need to specifically mark the templates they resolve as using decoupled logic.

Except for `StringTemplateResolver` (which does not allow decoupled logic), all other out-of-the-box implementations of `ITemplateResolver` will provide a flag called `useDecoupledLogic` that will mark all templates resolved by that resolver as potentially having all or part of its logic living in a separate resource:
```java
final ServletContextTemplateResolver templateResolver = 
        new ServletContextTemplateResolver(servletContext);
...
templateResolver.setUseDecoupledLogic(true);
```