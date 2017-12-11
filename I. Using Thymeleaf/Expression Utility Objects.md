### 表达式工具对象

除了这些基本的对象，Thymeleaf还会提供给我们一套工具对象，帮助我们在表达式里执行常见的任务。

- `#execInfo`: 与处理中的模版有关的信息
- `#messages`: 在变量表达式内部包含外部化信息的方法，与使用#{…}语法时相同
- `#uris`: 转义URLs/URIs部分的方法
- `#conversions`: 执行配置好的转换服务的方法（如果有的话）
- `#dates`: methods for `java.util.Date` objects: formatting, component extraction, etc.
- `#calendars`: analogous to `#dates`, but for `java.util.Calendar` objects.
- `#numbers`: methods for formatting numeric objects.
- `#strings`: methods for `String` objects: contains, startsWith, prepending/appending, etc.
- `#objects`: methods for objects in general.
- `#bools`: methods for boolean evaluation.
- `#arrays`: methods for arrays.
- `#lists`: methods for lists.
- `#sets`: methods for sets.
- `#maps`: methods for maps.
- `#aggregates`: methods for creating aggregates on arrays or collections.
- `#ids`: methods for dealing with id attributes that might be repeated (for example, as a result of an iteration).

你可以在[附录B](http://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#appendix-b-expression-utility-objects)里查看这些工具对象提供了哪些功能。