### 可遍历值

`java.util.List`类并不是Thymeleaf里唯一可以用于遍历的值。有相当完整的一套对象，可以用于`th:each`属性的遍历：

- 任何实现`java.util.Iterable`的对象
- 任何实现`java.util.Enumeration`的对象
- Any object implementing `java.util.Iterator`, whose values will be used as they are returned by the iterator, without the need to cache all values in memory.
- Any object implementing `java.util.Map`. When iterating maps, iter variables will be of class `java.util.Map.Entry`.
- Any array.
- Any other object will be treated as if it were a single-valued list containing the object itself.