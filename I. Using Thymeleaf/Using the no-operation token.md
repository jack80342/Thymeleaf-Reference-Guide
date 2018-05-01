### 使用无操作标记

如果只想让我们的片段把它目前的标记作为默认值，我们也可以使用无操作标记，把它作为传递给片段的参数。再一次使用`common_header`的例子：
```html
...
<head th:replace="base :: common_header(_,~{::link})">

  <title>Awesome - Main</title>

  <link rel="stylesheet" th:href="@{/css/bootstrap.min.css}">
  <link rel="stylesheet" th:href="@{/themes/smoothness/jquery-ui.css}">

</head>
...
```
看👀`title`参数（`common_header`片段的第一个参数）设置成了无操作标记 （`_`）， 这使得片段的这个部分没有被执行（`title`=无操作）：
```html
  <title th:replace="${title}">The awesome application</title>
```
所以最后就是：
```html
...
<head>

  <title>The awesome application</title>

  <!-- Common styles and scripts -->
  <link rel="stylesheet" type="text/css" media="all" href="/awe/css/awesomeapp.css">
  <link rel="shortcut icon" href="/awe/images/favicon.ico">
  <script type="text/javascript" src="/awe/sh/scripts/codebase.js"></script>

  <link rel="stylesheet" href="/awe/css/bootstrap.min.css">
  <link rel="stylesheet" href="/awe/themes/smoothness/jquery-ui.css">

</head>
...
```