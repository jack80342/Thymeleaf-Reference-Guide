### 表达式工具对象

除了这些基本的对象，Thymeleaf还会提供给我们一套工具对象，帮助我们在表达式里执行常见的任务。

- `#execInfo`: 与处理中的模版有关的信息
- `#messages`: 在变量表达式内部包含外部化信息的方法，与使用#{…}语法时相同
- `#uris`: 转义URLs/URIs部分的方法
- `#conversions`: 用于执行配置好的转换服务（如果有的话）
- `#dates`: 用于`java.util.Date`对象的方法：格式化、组件提取，等等
- `#calendars`: 类似与`#dates`，但是用于`java.util.Calendar`对象
- `#numbers`: 用于格式化数值对象
- `#strings`: 用于`String`对象：contains, startsWith, prepending/appending，等等
- `#objects`: 用于一般的对象
- `#bools`: 用于布尔求值
- `#arrays`: 用于数组
- `#lists`: 用于列表
- `#sets`: 用于集合
- `#maps`: 用于映射
- `#aggregates`: 用于计算数组或者列表的总量
- `#ids`: 用于处理可能重复的id属性（比如，迭代的结果）

你可以在[附录B](http://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#appendix-b-expression-utility-objects)里查看这些工具对象提供了哪些功能。