# Design patterns about business logic partitioning

## Mediator
Cons: implementation is hidden inside the mediator

```java
public enum Event {
    CLICK,
    LOGIN,
    AUTH,
}

public interface Component {
    private MediatorExample mediator;

    public Component(Mediator mediator);

    // At some point this.mediator.notify(this, Event.CLICK);
}

public interface Mediator {
    public void notify(Component sender, Event event);
}

public class MediatorExample implements Mediator {
    private Button btn1, btn2;
    private TextLabel title, subtitle;
    private TextBox name, surname, email;
    // ...
    
    public MediatorExample(
        Button b1, Button b2,
        TextLabel title, TextLabel subtitle,
        TextBox name, TextBox surname, TextBox emal
    ) {
        // register managed components
    }

    public void notify(Component sender, String event) {
        switch(sender) {
            case btn1: return btn1Medaiator(event);    
            case btn2: return btn1Medaiator(event);    
            // ..
        }
    }

    private void btn1Mediator(Event e) {
        switch(e)  {
            case CLICK: // ...
            // ...
        }
    }
    
    // ...
}
```

## MVC
TODO

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
> Goal: a consistent family of objects

```java
public interface IButton { ... }
public interface IEditor { ... }
public interface ITitle { ... }

// Concrete implementations of IButton, IEditor, ITitle

public interface IGuiFactory {
    public ITitle createTitle(String t);
    public IEditor createEditor(...);
    public IButton createButton(String t, Consumer<Event> f);
}

public class FlatGuiFactory implements IGuiFactory { ... }
public class MaterialGuiFactory implements IGuiFactory { ... }
// Other styles
```

## Strategy
> Goal: algorithm modularity with interchangable objects (containing the implementation) compliant to the same interface

```java
public interface SortStrategy<T> {
    public void sort(T[] array);
}

public class BubbleSort implements SortStrategy { ... }
public class MergeSort implements SortStrategy { ... }

public class Context<T> {
    private Strategy sortAlgo;

    public void setStrategy(Strategy s) {
        sortAlgo = s;
    }

    public void runStrategy(T ) {
    }
}
```
