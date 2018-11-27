## 常用的日志框架
1. j.u.l（java.util.logging包的简称）

2. Log4j

3. LogBack

4. Log4j2

## 日志门面 (便于解耦)：屏蔽了底层日志框架的具体实现，解除了应用与日志框架之间的耦合
1. SLF4j(Simple Logging Facade for Java，缩写SLF4J)
> 只是一个门面服务，不是真正的的日志框架，依赖 Log4j、logback 等日志框架

**计算机科学领域的任何问题都可以通过增加一个间接的中间层来解决。而门面模式就是对于这句话的典型实践。**