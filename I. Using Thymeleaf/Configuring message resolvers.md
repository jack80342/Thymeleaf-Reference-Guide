### 配置信息解析器

如果我们想往模板引擎里添加一个或者多个模板解析器，该怎么做呢？简单。
```java
// For setting only one
templateEngine.setMessageResolver(messageResolver);

// For setting more than one
templateEngine.addMessageResolver(messageResolver);
```
我们为什么想要有多个信息解析器呢？和模板解析器的原因相同：信息解析器有先后顺序。如果第一个信息解析器无法解析一条特定的信息，就会请求第二个，然后再是第三个······
