### 使用空片段

一种特殊的分段表达式——空片段（`~{}`），可以用于不🈯️定标记。使用之前的例子：
```html
<head th:replace="base :: common_header(~{::title},~{})">

  <title>Awesome - Main</title>

</head>
...
```
注意片段的第二个参数（`links`）设置成了🈳️片段。因此，`<th:block th:replace="${links}" />`的地方什么也没有：
```html
...
<head>

  <title>Awesome - Main</title>

  <!-- Common styles and scripts -->
  <link rel="stylesheet" type="text/css" media="all" href="/awe/css/awesomeapp.css">
  <link rel="shortcut icon" href="/awe/images/favicon.ico">
  <script type="text/javascript" src="/awe/sh/scripts/codebase.js"></script>

</head>
...
```