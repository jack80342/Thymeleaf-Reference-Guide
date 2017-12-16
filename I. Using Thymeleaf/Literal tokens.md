### 字面量标记

Numeric, boolean and null literals are in fact a particular case of literal tokens.

These tokens allow a little bit of simplification in Standard Expressions. They work exactly the same as text literals (`'...'`), but they only allow letters (`A-Z` and `a-z`), numbers (`0-9`), brackets (`[` and `]`), dots (`.`), hyphens (`-`) and underscores (`_`). So no whitespaces, no commas, etc.

The nice part? Tokens don’t need any quotes surrounding them. So we can do this:
```html
<div th:class="content">...</div>
```
instead of:
```html
<div th:class="'content'">...</div>
```