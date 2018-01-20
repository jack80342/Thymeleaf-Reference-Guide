### 可遍历值

The `java.util.List` class isn’t the onlyvalue that can be used for iteration in Thymeleaf. There is a quite complete set of objects that are considered iterable by a `th:each` attribute:

- Any object implementing `java.util.Iterable`
- Any object implementing `java.util.Enumeration`.
- Any object implementing `java.util.Iterator`, whose values will be used as they are returned by the iterator, without the need to cache all values in memory.
- Any object implementing `java.util.Map`. When iterating maps, iter variables will be of class `java.util.Map.Entry`.
- Any array.
- Any other object will be treated as if it were a single-valued list containing the object itself.