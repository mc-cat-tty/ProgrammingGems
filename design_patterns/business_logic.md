# Design patterns about business logic partitioning

## Mediator
Cons:
 - implementation is hidden inside the mediator



## MVC

## IOC and dependency injection
```java
public interface IService {
    public void service { ... }
}
```

```java
public class Server {
    public Server(IService s1, IService s2, ...) { ... }
}
```

## Builder
A waterfall of methods `withAttribute(val) -> ObjType` are used to tune the object insted of a constructor with all possible parameters and options.
Way better than setters.

## Abstract Factory

## Strategy

