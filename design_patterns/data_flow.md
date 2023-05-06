# Design patterns about data flows
## Observer
> Also called publish-subscriber, a _broker_ class is used to dispatch events among different _subscriber_ objects.

```java
public abstract class Event<IObserver> {
    protected final List<IObserver> observers;

    public Event() {
        observers = Collections.synchronizedList(new ArrayList<>());
    }

    public void attachObserver(IObserver observer) {
        synchronized (observers) {
            observers.add(observer;)
        }
    }

    public void detachObserver(IObserver observer) {
        synchronized (observers) {
            observers.remove(observer);
        }
    }
}
```

```java
public class Broker {
    private static Broker instance;  // singleton
    private final Event addEvent;
    private final Event deleteEvent;

    private Broker() {
        addEvent = new Event();
        deleteEvent = new Event();
    }

    public static Broker getInstance() {
        if (instance == null) {
            instance = new Broker();
        }
        return instance;
    }

    public Event getAddEvent() {
        return addEvent;
    }

    public Event getDeleteEvent() {
        return deleteEvent;
    }
}
```

## Stream
