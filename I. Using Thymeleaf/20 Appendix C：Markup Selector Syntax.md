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

Advanced attribute selection features:

- Besides = (equal), other comparison operators are also valid: `!=` (not equal), `^=` (starts with) and `$=` (ends with). For example: `x[@class^='section']` means elements with name `x` and a value for attribute `class` that starts with `section`.

- Attributes can be specified both starting with `@` (XPath-style) and without (jQuery-style). So `x[z='v']` is equivalent to `x[@z='v']`.

- Multiple-attribute modifiers can be joined both with `and` (XPath-style) and also by chaining multiple modifiers (jQuery-style). So `x[@z1='v1' and @z2='v2']` is actually equivalent to `x[@z1='v1'][@z2='v2']` (and also to `x[z1='v1'][z2='v2']`).

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
