### 4 标准表达式语法

我们将暂停开发我们的虚拟杂货店，来学习Thymeleaf标准方言里最重要的部分：Thymeleaf标准表达式语法。

我们已经看过了两种有效的表达属性值的语法：信息和变量表达式。如下：
```html
<p th:utext="#{home.welcome}">Welcome to our grocery store!</p>

<p>Today is: <span th:text="${today}">13 february 2011</span></p>
```
然而，还有更多类型的表达式，甚至已经学习过的表达式也还有更多有趣的细节需要学习。首先，让我们看看对标准表达式特性的总结：

- Simple expressions:
    - Variable Expressions: `${...}`
    - Selection Variable Expressions: `*{...}`
    - Message Expressions: `#{...}`
    - Link URL Expressions: `@{...}`
    - Fragment Expressions: `~{...}`
- Literals
    - Text literals: 'one text', 'Another one!',…
    - Number literals: `0`, `34`, `3.0`, `12.3`,…
    - Boolean literals: `true`, `false`
    - Null literal: `null`
    - Literal tokens: `one`, `sometext`, `main`,…
- Text operations:
    - String concatenation: `+`
    - Literal substitutions: `|The name is ${name}|`
- Arithmetic operations:
    - Binary operators: `+`, `-`, `*`, `/`, `%`
    - Minus sign (unary operator): `-`
- Boolean operations:
    - Binary operators: `and`, `or`
    - Boolean negation (unary operator): `!`, `not`
- Comparisons and equality:
    - Comparators: `>`, `<`, `>=`, `<=` (`gt`, `lt`, `ge`, `le`)
    - Equality operators: `==`, `!=` (`eq`, `ne`)
- Conditional operators:
    - If-then: `(if) ? (then)`
    - If-then-else: `(if) ? (then) : (else)`
    - Default: `(value) ?: (defaultvalue)`
- Special tokens:
    - No-Operation: `_`

All these features can be combined and nested:
```
'User is of type ' + (${user.isAdmin()} ? 'Administrator' : (${user.type} ?: 'Unknown'))
```