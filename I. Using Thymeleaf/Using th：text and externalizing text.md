### 使用th:text以及外部化文本

外部化文本就是从模版文件里取出一段模版代码，放到独立的文件里（通常是`.properties`文件）。这样，用其它语言写的等价文本就能很容易地代替它们。这个过程就是所谓的国际化，或者简单地称为i18n。外部化的代码片段通常称为“信息（message）”。

信息总是有一个键值，用来识别它们。Thymeleaf允许你指定：一段文本应当对应于一条特定的使用`#{...}`语法的信息。如下：
```html
<p th:text="#{home.welcome}">Welcome to our grocery store!</p>
```
我们在这儿看到的，实际上是Thymeleaf标准方言的两种不同的特性：

- `th:text`属性，会对其表达式求值，并把结果设置为宿主标签的主体，实际上会替换代码里的“Welcome to our grocery store!”文本。

- `#{home.welcome}`表达式，由标准表达式语法指定，指明：`th:text`属性使用的文本应当对应于键值`home.welcome`的信息。而键值`home.welcome`对应于我们处理模版时所在的地区。

那么，外部化的文本在哪里呢？

在Thymeleaf里，外部化的文本所在的位置完全可以配置。它取决于正在使用的指定的`org.thymeleaf.messageresolver.IMessageResolver`实现。通常，会使用基于`.properties`文件的实现。但是，如果想要，我们也可以创建我们自己的实现。比如，从数据库获🉐️信息。

然而，我们并没有在初始化的时候，为我们的模版引擎指定一个信息解析器。也就是说，我们的应用正在使用`标准信息解析器`。它由`org.thymeleaf.messageresolver.StandardMessageResolver`实现。

标准信息解析器期望在相同文件夹下的属性文件里，为`/WEB-INF/templates/home.html`找到信息。而且，属性文件需要和模版同名，比如：

- `/WEB-INF/templates/home_en.properties`对应🇬🇧英文文本。
- `/WEB-INF/templates/home_es.properties`对应🇪🇸西班牙文文本。
- `/WEB-INF/templates/home_pt_BR.properties`对应🇵🇹葡萄牙文（🇧🇷巴西文）文本。
- `/WEB-INF/templates/home.properties`对应默认文本（如果地区没有匹配项）。

让我们看一看我们的`home_es.properties`文件：
```properties
home.welcome=¡Bienvenido a nuestra tienda de comestibles!
```
这就是为了让Thymeleaf处理我们的模版，所要做的所有工作。接下来，让我们创建我们的Home controller。