### 可遍历值

`java.util.List`类并不是Thymeleaf里唯一可以用于遍历的值。有相当完整的一套对象，可以用于`th:each`属性的遍历：

- 任何实现`java.util.Iterable`的对象
- 任何实现`java.util.Enumeration`的对象
- 任何实现`java.util.Iterator`的对象，它的值会被使用，因为它们由遍历器返回，不需要在内存中缓存所有值。
- 任何实现`java.util.Map`的对象。当遍历map时，遍历变量是`java.util.Map.Entry`类
- 任何数组
- Any other object will be treated as if it were a single-valued list containing the object itself.