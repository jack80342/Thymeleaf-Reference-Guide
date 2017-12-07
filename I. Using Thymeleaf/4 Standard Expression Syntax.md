### 4 标准表达式语法

We will take a small break in the development of our grocery virtual store to learn about one of the most important parts of the Thymeleaf Standard Dialect: the Thymeleaf Standard Expression syntax.

We have already seen two types of valid attribute values expressed in this syntax: message and variable expressions:
```html
<p th:utext="#{home.welcome}">Welcome to our grocery store!</p>

<p>Today is: <span th:text="${today}">13 february 2011</span></p>
```
But there are more types of expressions, and more interesting details to learn about the ones we already know. First, let’s see a quick summary of the Standard Expression features:

- Simple expressions:
    - Variable Expressions: `${...}`
    - Selection Variable Expressions: `*{...}`
    - Message Expressions: `#{...}`
    - Link URL Expressions: `@{...}`
    - Fragment Expressions: `~{...}`
- Literals
    - Text literals: 'one text', 'Another one!',…
    - Number literals: `0`, `34`, `3.0`, `12.3`,…
    - Boolean literals: true, false
    - Null literal: null
    - Literal tokens: one, sometext, main,…
- Text operations:
    - String concatenation: +
    - Literal substitutions: |The name is ${name}|
- Arithmetic operations:
    - Binary operators: +, -, *, /, %
    - Minus sign (unary operator): -
- Boolean operations:
    - Binary operators: and, or
    - Boolean negation (unary operator): !, not
- Comparisons and equality:
    - Comparators: >, <, >=, <= (gt, lt, ge, le)
    - Equality operators: ==, != (eq, ne)
- Conditional operators:
    - If-then: (if) ? (then)
    - If-then-else: (if) ? (then) : (else)
    - Default: (value) ?: (defaultvalue)
- Special tokens:
    - No-Operation: _

All these features can be combined and nested:
```
'User is of type ' + (${user.isAdmin()} ? 'Administrator' : (${user.type} ?: 'Unknown'))
```