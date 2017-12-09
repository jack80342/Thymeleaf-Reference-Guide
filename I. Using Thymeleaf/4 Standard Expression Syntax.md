### 4 标准表达式语法

我们将暂停开发我们的虚拟杂货店，来学习Thymeleaf标准方言里最重要的部分：Thymeleaf标准表达式语法。

我们已经看过了两种有效的表达属性值的语法：信息和变量表达式。如下：
```html
<p th:utext="#{home.welcome}">Welcome to our grocery store!</p>

<p>Today is: <span th:text="${today}">13 february 2011</span></p>
```
然而，还有更多类型的表达式，甚至已经学习过的表达式也还有更多有趣的细节需要学习。首先，让我们看看对标准表达式特性的总结：

- 简单表达式：
    - 变量表达式： `${...}`
    - 选择变量表达式： `*{...}`
    - 信息表达式： `#{...}`
    - 链接URL表达式： `@{...}`
    - 分段表达式： `~{...}`
- 字面量
    - 文本字面量： 'one text', 'Another one!',…
    - 数字字面量： `0`, `34`, `3.0`, `12.3`,…
    - 布尔字面量： `true`, `false`
    - Null字面量： `null`
    - 字面量标记：`one`, `sometext`, `main`,…
- 文本运算：
    - 字符串拼接： `+`
    - 字面量置换: `|The name is ${name}|`
- 算术运算：
    - 二元运算符： `+`, `-`, `*`, `/`, `%`
    - 负号（一元运算符）： (unary operator): `-`
- 布尔运算：
    - 二元运算符： `and`, `or`
    - 布尔非（一元运算符）： `!`, `not`
- 比较和相等：
    - 比较： `>`, `<`, `>=`, `<=` (`gt`, `lt`, `ge`, `le`)
    - 相等运算符： `==`, `!=` (`eq`, `ne`)
- 条件运算符：
    - If-then: `(if) ? (then)`
    - If-then-else: `(if) ? (then) : (else)`
    - Default: `(value) ?: (defaultvalue)`
- 特殊标记：
    - 无操作： `_`

所有这些特性可以结合或者嵌套：
```
'User is of type ' + (${user.isAdmin()} ? 'Administrator' : (${user.type} ?: 'Unknown'))
```