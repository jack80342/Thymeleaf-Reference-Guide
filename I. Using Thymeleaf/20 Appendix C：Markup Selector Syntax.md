### 20 附录C：标记选择器语法

Thymeleaf的标记选择器直接借自Thymeleaf的句法分析库：[AttoParser](http://attoparser.org/)。

这些选择器的语法与XPath、CSS、jQuery里的选择器的语法很是相似。这使它们对大多数用户来说，容易上手。你可以在[AttoParser文档](http://www.attoparser.org/apidocs/attoparser/2.0.4.RELEASE/org/attoparser/select/package-summary.html)上看看完整的语法。

比如，下面的选择器会选择标记里的每个位置上，每一个带有class属性并且其值为`content`的`<div>`（注意这没有尽可能的简洁，继续读下去你就会知道为什么）：

```html
<div th:insert="mytemplate :: //div[@class='content']">...</div>
```

它的基本语法包括：

- `/x`：当前名为x的节点的直接的子节点。

- `//x`：当前名为x的节点在任何深度上的子节点。

- `x[@z="v"]`：名为x的元素，并且此元素有名为z、值为“v”的属性。

- `x[@z1="v1" and @z2="v2"]`：名为x的元素，并且此元素有名为z1、值为“v1”的属性和名为z2、值为“v2”的属性。

- `x[i]`：在名为x的元素的同级节点上，位于数字i上的元素。

- `x[@z="v"][i]`：在名为x、含有值为“v”的属性z的元素的同级节点上，位于数字i上的元素。

但是也可以使用更为简洁的语法：

- `x`与`//x`完全等价（在任何深度上搜索名字或者引用为`x`的元素，当是`th:ref`或者`th:fragment`时则为引用）。

- 选择器允许没有元素名/引用，只要它们包含有参数说明。所以，`[@class='oneclass']`是一个有效的选择器。它会寻找任何带有class属性并且值为`"oneclass"`的元素（标签）。

高级属性选择特性：

- 除了`=`（相等），另外的比较运算符同样有效：`!=`（不相等），`^=`（以······开头）以及`$=`（以······结束）。例如：`x[@class^='section']`表示名为`x`，属性`class`的值以`section`开头的元素。

- 属性既可以以`@`开头（XPath风格）的方式指定，也可以不加`@`（jQuery风格）。所以，`x[z='v']`与`x[@z='v']`是等价的。

- 多属性修饰符可以用`and`（XPath风格）连接，也可以通过链接多个修饰符（jQuery风格）连接。所以，`x[@z1='v1' and @z2='v2']`实际上等价于 `x[@z1='v1'][@z2='v2']`（也等价于`x[z1='v1'][z2='v2']`）。

Direct jQuery-like selectors:

- `x.oneclass` is equivalent to `x[class='oneclass']`.

- `.oneclass` is equivalent to `[class='oneclass']`.

- `x#oneid` is equivalent to `x[id='oneid']`.

- `#oneid` is equivalent to `[id='oneid']`.

- `x%oneref` means `<x>` tags that have a `th:ref="oneref"` or `th:fragment="oneref"` attribute.

- `%oneref` means any tags that have a `th:ref="oneref"` or `th:fragment="oneref"` attribute. Note this is actually equivalent to simply `oneref` because references can be used instead of element names.

- Direct selectors and attribute selectors can be mixed: `a.external[@href^='https']`.

So the above Markup Selector expression:


```html
<div th:insert="mytemplate :: //div[@class='content']">...</div>
```

Could be written as:

```html
<div th:insert="mytemplate :: div.content">...</div>
```

Examining a different example, this:

```html
<div th:replace="mytemplate :: myfrag">...</div>
```

Will look for a `th:fragment="myfrag"` fragment signature (or `th:ref` references). But would also look for tags with name `myfrag` if they existed (which they don’t, in HTML). Note the difference with:

```html
<div th:replace="mytemplate :: .myfrag">...</div>
```

…which will actually look for any elements with `class="myfrag"`, without caring about `th:fragment` signatures (or `th:ref` references).
