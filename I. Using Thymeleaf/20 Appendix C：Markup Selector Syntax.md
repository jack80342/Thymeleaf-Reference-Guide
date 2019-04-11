### 20 附录C：标记选择器语法

Thymeleaf’s Markup Selectors are directly borrowed from Thymeleaf’s parsing library: [AttoParser](http://attoparser.org/).

The syntax for this selectors has large similarities with that of selectors in XPath, CSS and jQuery, which makes them easy to use for most users. You can have a look at the complete syntax reference at the [AttoParser documentation](http://www.attoparser.org/apidocs/attoparser/2.0.4.RELEASE/org/attoparser/select/package-summary.html).

For example, the following selector will select every `<div>` with the class `content`, in every position inside the markup (note this is not as concise as it could be, read on to know why):

```html
<div th:insert="mytemplate :: //div[@class='content']">...</div>
```

The basic syntax includes:

- `/x` means direct children of the current node with name x.

- `//x` means children of the current node with name x, at any depth.

- `x[@z="v"]` means elements with name x and an attribute called z with value “v”.

- `x[@z1="v1" and @z2="v2"]` means elements with name x and attributes z1 and z2 with values “v1” and “v2”, respectively.

- `x[i]` means element with name x positioned in number i among its siblings.

- `x[@z="v"][i]` means elements with name x, attribute z with value “v” and positioned in number i among its siblings that also match this condition.

But more concise syntax can also be used:

- `x` is exactly equivalent to `//x` (search an element with name or reference `x` at any depth level, a reference being a `th:ref` or a `th:fragment` attribute).

- Selectors are also allowed without element name/reference, as long as they include a specification of arguments. So `[@class='oneclass']` is a valid selector that looks for any elements (tags) with a class attribute with value `"oneclass"`.

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
