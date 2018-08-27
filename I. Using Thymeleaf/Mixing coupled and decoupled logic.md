### 混合耦合的与解耦的逻辑

即使启用，解耦的模板逻辑也不是必须的。 When enabled, it means that the engine will look for a resource containing decoupled logic, parsing and merging it with the original template if it exists. No error will be thrown if the decoupled logic resource does not exist.

Also, in the same template we can mix both coupled and decoupled logic, for example by adding some Thymeleaf attributes at the original template file but leaving others for the separate decoupled logic file. The most common case for this is using the new (in v3.0) `th:ref` attribute.
